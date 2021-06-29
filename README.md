# DataPoiesis_publication_toolkit
An open source publication toolkit in which text becomes data ready to be visualized.

This is initialized with the publication of the [Datapoiesis project](https://www.he-r.it/project/datapoiesis-2/) (images have been removed).

To test it, you need a web server such as [Apache](https://httpd.apache.org/) or Node's command line webserver (just go in the folder of your HD where thet GIT repo is, and type http-server and you can use the browser to navigate locally)

# How does it work?

In the __data__ folder there is a __publication.json__ file.

It is the configuration file of the publication. 

Here you can configure stuff like the title and cover images.

Here and in the following: all paths are relative to the root folder of the git repository. 

You can place your images and chapters anywhere, just as long as you specify the right path on your filesystem, and that the files can be served from the webserver (for example: you cannot put the file oustide the webroot of your webserver).

Here in this example we have used a nice folder layout to keep things tidy.

# The sections

In the __publications.json__ file, you'll see a JSON array named __sections__: your section definitions go here.

Each section is a JSON object.

Sections are separated through a comma(,).

For example:

```
"sections": [

    {
			"title": "PREMESSA",
			"datafile": "sections/premessa.txt"
		},

		{
			"title": "INTRODUZIONE",
			"sections": [

				{
					"title": "(1) Datapoiesis. Il concept",
					"datafile": "sections/datapoies_il_concept.txt"
				}

			]
		},
    
    etccetera
    
```

Each section object has

* a __title__ and
* a __datafile__ that points to a markdown file

Section objects can define a hyerarchy of sections, meaning that they can have an embedded __sections__ array 

for example:

```
"sections": [
    {
      °title": "...",
      "datafile": "....",
      "sections": [
        {
          °title": "...",
          "datafile": "....",
          "sections": [
              ...
          ]
        },
        .....
      
      ]
    },
    ....
]
```

Look at the provided example for more formats.

# The Datafiles

The datafiles for the sections and subsections use markdown content similar to wikipedia. The exact markdown dialect is the one provided by [Showdown.js](http://showdownjs.com/)

# The Logic

the main software entry point is the __script.js__ file in the __js__ folder.

at the top these variables are defined.

```
var language = "italian";

var stopwordsfiles = {
	'italian': "assets/italian_stopwords.json",
	'engllish': "assets/english_stopwords.json",
	'others': "assets/others_stopwords.getJSON",
};
```

These define the current language and the __stopwords__, that are the words which you don't want to consider when doing text analysis.

The Datapoiesis happens in the __compute()__ function in the file. Currently it transforms the current section into a word network, but it could do other things as well.

__If you fork this repo to do other datapoietic interpretations of text, please notify us, so that we can build a credited list of datapoietic publications.__
