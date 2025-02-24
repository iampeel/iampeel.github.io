---
layout: post
title: Hello Hydeout
excerpt_separator:  <!--more-->
---



가나다라 마바사

public class Adapter_CheckBox extends BaseAdapter {
    private Context ctx;
    ArrayList<CheckListItem> datas = new ArrayList<CheckListItem>();
    private View.OnClickListener onClickListener;
    public Adapter_CheckBox(Context ctx, ArrayList<CheckListItem> datas, View.OnClickListener onClickListener) {
        this.ctx = ctx;
        this.datas = datas;
        this.onClickListener = onClickListener;
    }

    @Override
    public int getCount() {
        return datas.size();
    }

    @Override
    public Object getItem(int position) {
        return datas.get(position);
    }

    @Override
    public long getItemId(int position) {
        return 0;
    }

    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        View v = convertView;
        ViewHolder holder = null;
        if( v == null ){
            holder = new ViewHolder();
            // View를 inflater 시켜준다.
            v = LayoutInflater.from(ctx).inflate(R.layout.row_cb_list, null);
            holder.cb = (CheckBox) v.findViewById(R.id.row_cb);
            holder.tv = (TextView) v.findViewById(R.id.row_tv);
            v.setTag(holder);
        }
        else {
            holder = (ViewHolder)v.getTag();
        }
        holder.tv.setText(datas.get(position).desc);
        holder.cb.setChecked(datas.get(position).isChecked);
        holder.tv.setOnClickListener(onClickListener);
        holder.cb.setOnClickListener(onClickListener);
        return v;
    }
    class ViewHolder {
        private CheckBox cb;
        private TextView tv;
    }
}

Hydeout updates the original [Hyde](https://github.com/poole/hyde)
theme for [Jekyll](http://jekyllrb.com) 3.x and adds new functionality.

### Keep It Simple

In keeping with the original Hyde theme, Hydeout aims to keep the overall
design lightweight and plugin-free. JavaScript is currently limited only
to Disqus and Google Analytics (and is only loaded if you provide configuration
variables).

Hydeout makes heavy use of Flexbox in its CSS. If Flexbox is not available,
the CSS degrades into a single column layout.

### Customization

Hydeout replaces Hyde's class-based theming with the use
of the following SASS variables:

```scss
$sidebar-bg-color: #202020 !default;
$sidebar-fg-color: white !default;
$sidebar-sticky: true !default;
$layout-reverse: false !default;
$link-color: #268bd2 !default;
```

To override these variables, create your own `assets/css/main.scss` file.
Define your own variables, then import in Hydeout's SCSS, like so:

```
---
# Jekyll needs front matter for SCSS files
---

$sidebar-bg-color: #ac4142;
$link-color: #ac4142;
$sidebar-sticky: false;
@import "hydeout";
```

See the [_variables](https://github.com/fongandrew/hydeout/blob/master/_sass/hydeout/_variables.scss) file for other variables
you can override.

You can also insert custom head tags (e.g. to load your own stylesheets) by
defining your own `_includes/custom-head.html` or insert tags at the end
of the body (e.g. for custom JS) by defining your own
`_includes/custom-foot.html`.

### New Features

* Hydeout also adds a new tags page (accessible in the sidebar) and a new
  "category" layout for dedicated category pages.

* Category pages are automatically added to the sidebar. All other pages
  must have `sidebar_link: true` in their front matter to show up in
  the sidebar.

* A simple redirect-to-Google search is available. If you want to use
  Google Custom Search or Algolia or something with more involved,
  override the `search.html`.

* Disqus integration is ready out of the box. Just add the following to
  your config file:

  ```yaml
  disqus:
    shortname: my-disqus-shortname
  ```

  If you don't want Disqus or want to use something else, override
  `comments.html`.

* For Google Analytics support, define a `google_analytics` variable with
  your property ID in your config file.

There's also a bunch of minor tweaks and adjustments throughout the
theme. Hope this works for you!
