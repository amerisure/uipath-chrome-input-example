# uipath-chrome-input-example

## Overview
This example shows how to prompt for input using Google Chrome instead of Internet Explorer in UiPath.

> **Note:** UiPath has released [a Forms activities package with a drag-and-drop form designer](https://forum.uipath.com/t/forms-activities-now-in-public-preview/129300) (in beta at the time of writing in September 2019). If you don't specifically need the capabilities of a browser, the Forms activities package may be a better fit. However, if you do need a browser (e.g., your form needs to make AJAX calls, use iframes, render charts, etc.), then this method should still be helpful.

![Demo](demo.gif)

This is *not* about launching an automation task in Google Chrome. UiPath already has a convenient built-in way to do that using the `Open Browser` activity. This is about showing a form that you need your UiPath workflow to collect user input from.

## Why Not Use `Custom Input`?
The `Custom Input` activity is UiPath's out-of-the-box way of prompting for complex user input. (You can prompt for simple input, a single string, through the `Input Dialog` activity.)

The problem with `Custom Input` is that it renders the webpage you specify in Internet Explorer 7. There's no way to change to another browser. This is a problem because...Internet Explorer 7.

## How the Workaround Works
This example launches Chrome using `Start Process`, then creates up a `System.Net.HttpListener` that waits for and returns user input.

Broken down further, the workflow's steps are:

1. Launch Google Chrome using the `Start Process` activity, passing the URL of your input form. (The input form is a local HTML file in the example, but you could use any protocol that Chrome supports.)
1. Run `Invoke Code` to start an HTTP listener on http://localhost:5005.
1. Wait for `POST`ed data.
1. Return the `POST`ed data as a string.

The local HTML file contains a simple form that loads Bootstrap. The OK button triggers a function that posts to http://localhost:5005.
