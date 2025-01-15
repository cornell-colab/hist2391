### IIIF Manifests:
{% assign manifests = site.static_files | where_exp: "manifest", "manifest.path contains '/manifests/'"  |where_exp: "manifest", "manifest.extname == '.json'" | where_exp: "manifest", "manifest.path != '/manifests/collection.json' " %}

{% for file in manifests %}
[{{ file.path | replace: "/manifests/", ""}}]({{ file.path | absolute_url }}) 
[View in Mirador](https://projectmirador.org/embed/?iiif-content={{ file.path | absolute_url}})
[View in UV](http://universalviewer.io/examples/#?c=&m=&s=&cv=&manifest={{ file.path | absolute_url}
