### Simple Server

In a terminal or prompt, use `cd` to navigate to a folder full of HTML content, and type the following:

```
http-server -p 8080
```

This will launch a server process on your computer. Note that you will lose the ability to control that previous terminal window, though you can open others.

In a web browser, you can now access:

```
http://localhost:8080/
```

You should see the contents of the folder! This should bypass local file and cross domain restrictions on your computers during local development. This effectively emulates your content being on a host server somewhere else, and so the browser is no longer accessing your local file system.

Make sure you use this technique when working with external files that your visualization needs to import.

-----

Now that we have an example loaded, let's [combine the data we've now loaded](maps.md).