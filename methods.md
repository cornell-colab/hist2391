# Methods for Creating and Hosting IIIF Images and Manifests Using GitHub

This guide walks you through three **free, easy** methods for creating and hosting [International Image Interoperability Framework (IIIF)](https://en.wikipedia.org/wiki/International_Image_Interoperability_Framework) manifests from images that you've downloaded to your local device. There are no fees for processing and hosting through any of these methods and all of the tools and applications used in these methods are open-source. The only requirements are an email address and a device with access to the Internet.

Note that all of these methods rely on tools and workflows created by IIIF Technical Coordinator [Glen Robson](https://github.com/glenrobson). Methods get progressively harder and more intensive as you go through this guide.

## Introduction: IIIF and Level-0 Compliance

The International Image Interoperability Framework describes itself as “a set of open standards for delivering high-quality, attributed digital objects online at scale.” Effectively, IIIF standardizes the way images are delivered by servers to platforms, tools, and environments on the Web using a series of Application Programming Interfaces (APIs) that allow two different computers or pieces of software to communicate with one another. Because IIIF’s Image API specifies exactly how an image’s pixels will be served to a viewer or user, it’s easy to specify exactly how much and in what way you want the image to be displayed. For more on how IIIF works, see [IIIF’s How It Works](https://iiif.io/get-started/how-iiif-works/#:~:text=IIIF%20is%20a%20way%20to,but%20cannot%20do%20much%20else.) guide.

Image servers can be compliant at different levels with the parameters needed to make them work with the IIIF Image API. In this guide, all of the images we produce will be Level-0 compliant, meaning that they have the minimum amount of information needed to make them work with version 2 or version 3 of the IIIF Image API. This restricts what area of the image you can specify in an image viewer. For more on compliance, see the [IIIF’s Image API Compliance, Version 3.0.0 documentation](https://iiif.io/api/image/3.0/compliance/).

An [International Image Interoperability Framework manifest](https://iiif.io/guides/using_iiif_resources/) is a package that contains all of the information about an image or group of images served using IIIF, including the metadata, order of presentation, size specifications, etc. for a digital object. Creating manifests for your images means that you can specify metadata about that image that will display when the manifest is viewed in a IIIF-compatible viewer. There are also tools, digital exhibition platforms, and viewers that only accept manifest URLs, not just image URIs, so knowing how to create compliant images *and* manifests is useful.

## Method 1: Internet Archive

The [Internet Archive](https://en.wikipedia.org/wiki/Internet_Archive), or archive.org, has a public upload feature that allows users to upload their own content to the Internet Archive [repository](https://en.wikipedia.org/wiki/Content_repository) and share it with others. Images uploaded this way are automatically IIIF compliant; [the Internet Archive has a partnership with IIIF](https://blog.archive.org/2023/09/18/making-iiif-official-at-the-internet-archive/), so the IIIF Image API is a built-in feature of the Internet Archive’s image service. This method only works if the image you're uploading is outside of [copyright](https://en.wikipedia.org/wiki/Copyright), is covered under a [Creative Commons license](https://en.wikipedia.org/wiki/Creative_Commons_license) (see [CC licenses](https://creativecommons.org/share-your-work/cclicenses/) for specific parameters for sharing), or is owned by you. Material with current copyrights cannot be shared this way, since all images are public.

To create an IIIF Manifest for an image using the Internet Archive:

1. Create an Internet Archive account using an email and password. Note that the Internet Archive experienced cyberattacks in 2024 that allowed hackers to steal user information, so we suggest being cautious when creating accounts. I do not suggest adding your full name or personal information to your account.  
2. Click the **Upload** button in the top right corner of the screen. Drag or select an image from your local machine to upload.  
3. Once the image has loaded, add metadata to your image. The following fields are required: Description and Subject Tags. The Identifier field will default to the filename of your image.   
4. Select “No” next to "Test Items"; this is required for this method to work.  
5. Click the **Upload and Create Your Item** button at the bottom of the screen. Wait for the image to load in a new tab.  
6. Scroll down on the new image page to the Identifier field. Copy the identifier.  
7. Paste the identifier into the following URL scheme, without the brackets: "https://iiif.archive.org/iiif/`IDENTIFIER`/manifest.json."
8. Paste the URL into a IIIF-supported viewer, such as [Universal Viewer](https://universalviewer.io) or [Mirador](https://mirador-dev.netlify.app/__tests__/integration/mirador/), to test it.

Since the image is hosted through the Internet Archive already, you do not need to host it separately. This process means that you can create a manifest for almost any image that has been uploaded to the Internet Archive, as long as you have its identifier.

## Method 2: IIIF Workbench in GitHub.com

In September 2024, the Internet Archive suspended its services temporarily [due to cyberattacks](https://www.forbes.com/sites/larsdaniel/2024/10/20/internet-archive-breached-again-third-cyber-attack-in-october-2024/). It became necessary to find an alternate method of rendering and serving IIIF manifests for free from personal photos, images found on the Web, or . A Cantaloupe or self-hosted server does not solve the problem, since this would have to be hosted by the Cornell Reclaim Hosting space (a paid space) to be able to share images across the web instead of my local computer server.

The caveats of this method are that IIIF Workbench is slow at rendering images with the tiler, so it can take a while for images to upload. IIIF Workbench also sometimes never generates tiles for an image—it just loads on "Generating tiles" forever, which you wouldn't be able to tell until you've already waited 15 minutes for your image to load. Lastly, it does not work with an organizational GitHub account because you can't log into organizational accounts. This means a lot of annoying manual file-editing and transferring once you've uploaded all of your images and manifests. Regardless, it is a free and useful alternative to the Internet Archive method.

1. Download images from your repository of choice. TIFFs are best, JPEG 2000s are the next best, and regular JPEGs are third best.  
2. Check the file sizes. Export images that are over 100mb to smaller JPEGs, as close to lossless as possible. If you're working on a Mac, you can do this in Preview by going to **File** \> **Export** and selecting JPEG.  
3. Log into a personal GitHub account.   
4. Open the [IIIF Workbench](https://workbench.gdmrdigital.com/login.xhtml). Allow access to your GitHub repositories.   
5. Create a new project and upload all images to the workbench, one by one.  
6. Wait five minutes or so for the images to process, generate tiles, upload to GitHub, and publish to the web. This may take a while, so try to have patience.  
7. After the images load, copy the `info.json` URI that is below each image.  
8. Open a manifest editor, such as the [Bodelain Manifest Editor](https://digital.bodleian.ox.ac.uk/manifest-editor/#/?_k=fsgx3h), in a browser and add a canvas.   
9. Copy the `info.json` URI for an image onto the canvas. This section depends on what manifest editor you are using. In the Bodleian Manifest Editor, you add images in the “Canvas Metadata” section.  
10. Manually add metadata for each image. I often copy the metadata from the repository catalog record, but you can determine your scheme and make your own fields.  
11. Save the manifest to your local machine.   
12. Upload the manifest file to the IIIF Workbench.  
13. Test the manifest URIs in a viewer, such as [Universal Viewer](https://universalviewer.io) or [Mirador](https://mirador-dev.netlify.app/__tests__/integration/mirador/).

If you want the manifests to be hosted by a personal GitHub account, you can stop here. However, if you would like them to be hosted by an organizational GitHub account, do the following:

1. Open the repository on GitHub and transfer ownership of the project repository. Alternatively, you can download all images and manifest files and reupload them to the organizational GitHub account one by one.  
2. Do a search in your repository for the personal account username. Edit files to remove the username for the personal GitHub account and replace it with organizational GitHub username. Commit your changes.  
3. Test manifest URLs in a viewer.

## Method 3: IIIF Tiler and GitHub.com

Method 3 using GitHub is slightly more hands-on, but cuts out IIIF Workbench as the middleman and thus lets the user take more ownership of their processing, metadata creation, etc. This method uses a Java-run iiif-tiler on your local machine, run through command prompts on your local device, to process the images into Level 0 IIIF-compliant images. It then uses GitHub to host those images and present them using the IIIF Presentation API through GitHub Pages.

If you are not yet familiar with how to use the command line on your device, please see [Ian Mulligan and James Baker’s Introduction to the Bash Command Line lesson](https://programminghistorian.org/en/lessons/intro-to-bash) on Programming Historian first.

This method is not for the faint of heart; it requires patience and attention to detail, but goes faster than the IIIF Workbench method:

1. Install Java on your machine. If you are on Mac, you can [use Homebrew to install Java](https://formulae.brew.sh/formula/openjdk) or [install Java from Java.com](http://Java.com). If you are on Windows, you can use the [official Java installation instructions from Java.com](http://Java.com).  
2. Create a directory `iiif-workshop` on your local device. You can name your folder something else, just make sure to edit the command in step 9 appropriately.  
3. Log into your organizational or personal GitHub account. Create a new repository.   
4. In the repository, create a “manifests” folder and an “images” folder.  
5. Download [`iiif-tiler.jar`](https://github.com/glenrobson/iiif-tiler/tree/main) to your device and drag it in your `iiif-workshop` directory.  
6. Download images from your repository of choice. TIFFs are best, JPEG 2000s are the next best, and JPEGs are third best.  
7. Make sure your file names are distinct. Files must have different names or the tiler will mix them up.  
8. Drag all of your images into the `iiif-workshop` directory.  
9. Change directories in a command prompt to the iiif-workshop directory: `cd ~/iiif-workshop`   
10. Run the command: `java -jar iiif-tiler.jar`  
11. Wait for a folder named `iiif` to appear in the `iiif-workshop directory`. When you open the new `iiif` folder, you'll find folders containing the tiles of each image and an `info.json` file.  
12. Create a new directory in your GitHub repository's images directory for each image. It's easiest to name the directory, the image, and the manifest all the same thing so you don't get confused.  
13. For each image, upload the `info.json` file and all tile files into the appropriately named GitHub directory. You may have to do this in batches, since GitHub has a cap on uploads with file size and amount.  
14. After all files have uploaded successfully, open the `info.json file` for each image and update the `@id` field to: “https://`YOUR-GITHUB-USERNAME`.github.io/`YOUR-REPO-NAME`/images/`YOUR-IMAGE-NAME`/”  
15. Open a manifest editor in a browser and add a canvas. Copy the `@id` above and add `/info.json` to the end. Paste this URI into the canvas.  
16. Manually add metadata for each image. I often copy the metadata from the repository catalog record, but you can determine your scheme and make your own fields.  
17. Save the manifest to your local machine.  
18. Upload the manifests to the manifests directory of your GitHub repository.  
19. Open each manifest file to correct the `@id` so that it reads: "https://`YOUR-GITHUB-USERNAME`.github.io/`YOUR-REPO-NAME`/manifests/`YOUR-IMAGE-NAME`/”  
20. Commit changes. Wait for the changes to finish processing.  
21. Test your new manifest URLs. Your new manifest URLs should be the same as the `@id` field you just edited in step 19\.

## Method 4: libvips and GitHub.com

Method 4 is very similar to Method 3, but uses libvips, an image-processing library, instead of IIIF-Tiler to create Level 0 IIIF-compliant image tiles. It then uses GitHub to host those images and present them using the IIIF Presentation API through GitHub Pages.

1. Install libvips to your local machine. Follow the [libvips installation instructions](https://www.libvips.org/install.html).  
2. Log into your organizational or personal GitHub.com account.  
3. Create a new repository. In the repository, create a `manifests` folder and an `images` folder.  
4. On your local machine, create a new folder to store all of your images.  
5. Download images from your repository of choice. TIFFs are best, JPEG 2000s are the next best and JPEGs are third best.  
6. Place all images in the folder you created in step 3\.  
7. Open the command line. Change directories to the directory that your image is in, e.g.: `cd Downloads`  
8. Run a command: `vips dzsave yourimagename --layout iiif mypyr.zip`  
9. Wait for a folder named `mypyr.zip` to appear on your computer. When you open the zip file, you'll find folders containing the tiles of your image and an `info.json` file.  
10. Create a new folder in your GitHub repository's images folder for each image. Going forward, it's easiest to name the image folder and the manifest the same thing so you don't get confused.  
11. For each image, upload the `info.json file` and all tile files into the appropriately named image folder in your GitHub repository. You may have to do this in batches, since GitHub has a cap on uploads with file size and amount.  
12. After all files have uploaded successfully, open the info.json file for each image and update the `@id` field to: “https://`YOUR-GITHUB-USERNAME`.github.io/`YOUR-REPO-NAME`/images/`YOUR-IMAGE-NAME`/”  
13. Open a manifest editor in a browser and add a canvas. Copy the `@id` above and add `/info.json` to the end. Paste this URI into the canvas.  
14. Manually add metadata for each image. I often copy the metadata from the repository catalog record, but you can determine your scheme and make your own fields.  
15. Save the manifest to your local machine.  
16. Upload the manifests to the manifests directory of your GitHub repository.  
17. Open each manifest file to correct the `@id` so that it reads: “https://`YOUR-GITHUB-USERNAME`.github.io/`YOUR-REPO-NAME`/manifests/`YOUR-IMAGE-NAME`/”  
18. Commit changes. Wait for the changes to finish processing.  
19. Test your new manifest URLs. Your new manifest URLs should be the same as the `@id` field you just edited in step 17\.

Note that these methods are just some of the easiest ways you can use various programs to create static tiles and Level-0 compliant images. Given the pervasiveness and usefulness of IIIF for serving and presenting images, there are plenty of Python, Ruby, and Javascript libraries and tools for generating tiles. For more tools, see the community-built [Awesome IIIF GitHub repository](https://github.com/IIIF/awesome-iiif?tab=readme-ov-file#image-servers).
