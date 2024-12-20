This site holds all of the IIIF manifests and images processed by the Digital CoLab for HIST 22391: From Terra Incognita to Territories of Nation-States: Early American History in Two Dozen Maps. Manifests are ordered alphabetically and the labels will be the same as the individual image title in whatever repository the image is from.

### IIIF Manifests:
{% assign manifests = site.static_files | where_exp: "manifest", "manifest.path contains '/manifests/'"  |where_exp: "manifest", "manifest.extname == '.json'" | where_exp: "manifest", "manifest.path != '/manifests/collection.json' " %}

{% for file in manifests %}
 * [{{ file.path | replace: "/manifests/", ""}}]({{ file.path | absolute_url }}) 
    * [View in Mirador](https://projectmirador.org/embed/?iiif-content={{ file.path | absolute_url}})
    * [View in UV](http://universalviewer.io/examples/#?c=&m=&s=&cv=&manifest={{ file.path | absolute_url}})
{% endfor %}

### IIIF Images:
<details>
<summary>Images</summary>
<script src="{{ '/plugins/js/image.js' | absolute_url }}" ></script>

<script
			  src="https://code.jquery.com/jquery-3.5.1.min.js"
			  integrity="sha256-9/aliU8dGd2tb6OSsuzixeV4y/faTqgFtohetphbbj0="
			  crossorigin="anonymous"></script>
<link rel="stylesheet" href="plugins/justified/justifiedGallery.min.css" />
<script src="plugins/justified/jquery.justifiedGallery.min.js"></script>

<script>
{% assign files = site.static_files | where_exp: "image", "image.path contains '/images/'" |where_exp: "image", "image.path contains '/info.json'"   %}
{% for img_file in files %}
    addToGallery('gallery', '{{img_file.path | absolute_url}}', 300,300);
{% endfor %}
</script>
<div id="gallery">
        
</div>

<script>
    $("#gallery").justifiedGallery({
        rowHeight: 300
    });
</script>
</details>

