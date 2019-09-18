# uipath-chrome-input-example
This example shows how to prompt a UiPath user for complex input using Google Chrome.

UiPath's out-of-the-box way of prompting for complex input is through the `Custom Input` activity. This activity renders the webpage you specify in an embedded Internet Explorer 7 instance. This is a problem because Internet Explorer 7.

There's no way to change which browser `Custom Input` uses, so this workaround uses a local HTTP listener instead.

## How It Works

The workflow does the following:

1. Launches Google Chrome using the `Start Process` activity, passing the URL of your input form. (The input form is a local HTML file in the example, but you could use any protocol that Chrome supports.)
1. Runs `Invoke Code` to start an HTTP listener on http://localhost:5005.
1. Waits for `POST`ed data.
1. Returns the `POST`ed data as a string.

The local HTML file contains a simple form that loads Bootstrap. The OK button triggers a function that posts to http://localhost:5005.
