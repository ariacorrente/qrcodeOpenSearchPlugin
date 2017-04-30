# Development notes

Notes to self.

## How to test the search plugin on Firefox

Solution found thanks to the following documentation:

- [Creating OpenSearch plugins for Firefox](https://developer.mozilla.org/en-US/Add-ons/Creating_OpenSearch_plugins_for_Firefox#Autodiscovery_of_search_plugins)
- [Adding search engines from Web pages](https://developer.mozilla.org/en-US/docs/Web/API/Window/sidebar/Adding_search_engines_from_Web_pages#Installing_OpenSearch_plugins)

It's possible to install locally an addon for Firefox but I have not found a
way to do the same with a search engine. I tried saving the XML file into the
`searchplugins` folder but the engine will not be detected.

The only supported way appears to be publishing the search engine on a web page.
In the documentation I found two methods.

Using the `<link>` method is complex because the web server must serve the
XML file with a specific MIME and other stuff like that.

The javascript function have lesser requirements, the XML file must only be
available from an HTTP connection. I wrote a simple HTML page containing the
javascript code needed to install the search engine, the only info required
is a link to the XML file. The link must be in absolute format, something like
`http://my-server.com/my-folder/qrcode.xml`, **not** a relative URL.

This is the procedure:

1. upload `qrcode.xml` somewhere, for example a local web server, a cloud
    service, an owncloud instance ora a pastbin. The only requirement is a
    direct link. Even easier, use the python's SimpleHTTPServer to create an
    HTTP server on localhost
2. open the file `test/test.html` with your browser
3. put the absolute URL of `qrcode.xml` in the text filed and push the button
    below
4. when asked, confirm the installation of the search plugin. You may need to
    remove the previous version.
