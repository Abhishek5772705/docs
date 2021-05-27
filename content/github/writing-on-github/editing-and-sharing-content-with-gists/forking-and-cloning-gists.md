---
title: Forking and cloning gists
intro: 'Gists are actually Git repositories, which means that you can fork or clone any gist, even if you aren''t the original author. You can also view a gist''s full commit history, including diffs.'
redirect_from:
  - /articles/forking-and-cloning-gists
  - /github/writing-on-github/forking-and-cloning-gists
versions:
  free-pro-team: '*'
  enterprise-server: '*'
  github-ae: '*'
---
### Forking gists

Each gist indicates which forks have activity, making it easy to find interesting changes from others.

![Gist forks](/assets/images/help/gist/gist_forks.png)

### Cloning gists

If you want to make local changes to a gist and push them up to the web, you can clone a gist and make commits the same as you would with any Git repository. For more information, see "[Cloning a repository](/articles/cloning-a-repository)."

![Gist clone button](/assets/images/help/gist/gist_clone_btn.png)

### Viewing gist commit history

To view a gist's full commit history, click the "Revisions" tab at the top of the gist{.

![Gist revisions tab](/assets/images/help/gist/gist_revisions_tab.png)

You will see a full commit history for the gist with diffs.

![Gist revisions page](/assets/images/help/gist/gist_history.png)

 
What is Pipedream?
Support and Community
Signing Up
Plans and Pricing
Getting Started
What are workflows?
Your first workflow
Event Sources
What are Event Sources?
Logs
Workflow Steps
What are steps?
Triggers
Code
Workflow state
Make HTTP Requests with Node.js
Basic axios usage notes
Send a GET request to fetch data
Send a POST request to submit data
Pass query string parameters to a GET request
Send a request with HTTP headers
Send a request with a secret or API key
Send multiple HTTP requests using a loop
Send a multipart/form-data request
Download a file to the /tmp directory
Upload a file from the /tmp directory
Use an HTTP proxy to proxy requests through another host
IP addresses for HTTP requests made from Pipedream workflows
Forward an incoming HTTP request to another URL
Stream a downloaded file directly to another URL
Working with the filesystem in Node.js
Actions (legacy)
Params
Sharing code across workflows
Running asynchronous code
Workflow Events
What are events?
Inspect Events
Replay Events
Send Test Events
Managing Concurrency and Throttling
Cold Starts
Connecting to Apps
List of Integrated Apps
Connected Accounts
Auth in code steps
Errors
Common Errors
Global Error Workflow
Managing Workflows
Copying Workflows
Edit and Manage
Workflow Settings
Workflow Code and Data Visibility
Environment Variables
Components
Overview
Quickstart: Action Development
Quickstart: Source Development
Component API Reference
Contributing to the Pipedream Registry
Migrating from Legacy Actions to Component Actions
User Settings
Examples
Example: Add Rows to Google Sheets
Example: Delay a workflow before the next step runs
CLI
Installing the CLI
Logging into the CLI
CLI Reference
APIs
API Overview
Authentication
REST API
REST API Example: Webhooks
REST API example: Create an RSS source
REST API example: Workflow errors
Server-Sent Events (SSE)
Destinations
Overview
HTTP
Amazon S3
Email
Pipedream SQL Service
Emit events
Server-Sent Events (SSE)
Integrations
List of Integrated Apps
Discord
ServiceNow
Slack
Strava
Twitter
Zoom
Limits
New Features / Bugs
Privacy & Security
Privacy and Security at Pipedream
Security Best Practices
PGP Key
Subprocessors
Service Status
#Make HTTP Requests with Node.js
HTTP requests are fundamental to working with APIs or other web services. You can make HTTP requests to retrieve data from APIs, fetch HTML from websites, or do pretty much anything your web browser can do.

Below, we'll review how to make HTTP requests using Node.js code on Pipedream.

We'll use the axios and got HTTP clients in the examples below, but you can use any npm package you'd like on Pipedream, so feel free to experiment with other clients, too.

If you're new to HTTP, see our glossary of HTTP terms for a helpful introduction.

Basic axios usage notes
Send a GET request to fetch data
Send a POST request to submit data
Pass query string parameters to a GET request
Send a request with HTTP headers
Send a request with a secret or API key
Send multiple HTTP requests using a loop
Send a multipart/form-data request
Download a file to the /tmp directory
Upload a file from the /tmp directory
Use an HTTP proxy to proxy requests through another host
IP addresses for HTTP requests made from Pipedream workflows
Forward an incoming HTTP request to another URL
Stream a downloaded file directly to another URL
#Basic axios usage notes
To use axios on Pipedream, you'll just need to require the axios npm package:

const axios = require("axios");
You make HTTP requests by passing a JavaScript object to axios that defines the parameters of the request. For example, you'll typically want to define the HTTP method and the URL you're sending data to:

{
  method: "GET",
  url: `https://swapi.co/api/films/`
}
axios returns a Promise, which is just a fancy way of saying that it makes the HTTP request in the background (asynchronously) while the rest of your code runs. On Pipedream, all asynchronous code must be run synchronously, which means you'll need to wait for the HTTP request to finish before moving on to the next step. You do this by adding an await in front of the call to axios.

Putting all of this together, here's how to make a basic HTTP request on Pipedream:

const resp = await axios({
  method: "GET",
  url: `https://swapi.co/api/films/`,
});
The response object resp contains a lot of information about the response: its data, headers, and more. Typically, you just care about the data, which you can access in the data property of the response:

const resp = await axios({
  method: "GET",
  url: `https://swapi.co/api/films/`,
});

// HTTP response data is in the data property
const data = resp.data;
Alternatively, you can access the data using object destructuring, which is equivalent to the above and preferred in modern JavaScript:

const { data } = resp;
#Send a GET request to fetch data
Make a request to retrieve Star Wars films from the Star Wars API:

const axios = require("axios");

// Make an HTTP GET request using axios
const resp = await axios({
  method: "GET",
  url: `https://swapi.co/api/films/`,
});

// Retrieve just the data from the response
const { data } = resp;
Copy this workflow to run this example on Pipedream.

#Send a POST request to submit data
POST sample JSON to JSONPlaceholder, a free mock API service:

const axios = require("axios");

// Make an HTTP POST request using axios
const resp = await axios({
  method: "POST",
  url: `https://jsonplaceholder.typicode.com/posts`
  data: {
    name: "Luke",
  }
});

// Retrieve just the data from the response
const { data } = resp;
When you make a POST request, you pass POST as the method, and include the data you'd like to send in the data object.

Copy this workflow to run this example on Pipedream.

#Pass query string parameters to a GET request
Retrieve fake comment data on a specific post using JSONPlaceholder, a free mock API service. Here, you fetch data from the /comments resource, retrieving data for a specific post by query string parameter: /comments?postId=1.

const axios = require("axios");

// Make an HTTP GET request using axios
const resp = await axios({
  method: "GET",
  url: `https://jsonplaceholder.typicode.com/comments`,
  params: {
    postId: 1,
  },
});

// Retrieve just the data from the response
const { data } = resp;
You should pass query string parameters using the params object, like above. When you do, axios automatically URL-encodes the parameters for you, which you'd otherwise have to do manually.

Copy this workflow to run this code on Pipedream.

#Send a request with HTTP headers
You pass HTTP headers in the headers object of the axios request:

const axios = require("axios");

// Make an HTTP GET request using axios
const resp = await axios({
  method: "POST",
  url: `https://jsonplaceholder.typicode.com/posts`,
  headers: {
    "Content-Type": "application/json",
  },
  data: {
    name: "Luke",
  },
});
#Send a request with a secret or API key
Most APIs require you authenticate HTTP requests with an API key or other token. Please review the docs for your service to understand how they accept this data.

Here's an example showing an API key passed in an HTTP header:

const axios = require("axios");

// Make an HTTP GET request using axios
const resp = await axios({
  method: "POST",
  url: `https://jsonplaceholder.typicode.com/posts`,
  headers: {
    "Content-Type": "application/json",
    "X-API-Key": "123", // API KEY
  },
  data: {
    name: "Luke",
  },
});
Copy this workflow to run this code on Pipedream.

#Send multiple HTTP requests using a loop
There are many ways to make multiple HTTP requests. This code shows you a simple example that sends the numbers 1, 2, and 3 in the body of an HTTP POST request:

const axios = require("axios");

// We'll store each response and return them in this array
const responses = [];

for (const num of [1, 2, 3]) {
  const resp = await axios({
    method: "POST",
    url: params.url,
    data: {
      num, // Will send the current value of num in the loop
    },
  });
  responses.push(resp.data);
}

return responses;
This sends each HTTP request in sequence, one after another, and returns an array of response data returned from the URL to which you send the POST request.

Copy this workflow and fill in your destination URL to see how this works. This workflow iterates over the value of a Pipedream step export - data returned from a previous step. Since you often want to iterate over data returned from a Pipedream action or other code step, this is a common use case.

#Send a multipart/form-data request
const axios = require("axios");
const FormData = require("form-data");

const formData = new FormData();
formData.append("name", "Luke Skywalker");

const headers = formData.getHeaders();
const config = {
  method: "POST",
  url: params.url,
  headers,
  data: formData,
};
return await axios(config);
Copy this workflow to run this example.

#Download a file to the /tmp directory
This example shows you how to download a file to a file in the /tmp directory. This can be especially helpful for downloading large files: it streams the file to disk, minimizing the memory the workflow uses when downloading the file.

const fs = require("fs");
const got = require("got");
const stream = require("stream");
const { promisify } = require("util");

// DOWNLOAD
const pipeline = promisify(stream.pipeline);
await pipeline(
  got.stream(params.downloadURL),
  fs.createWriteStream(params.filePath)
);
Copy this workflow to run this example.

#Upload a file from the /tmp directory
This example shows you how to make a multipart/form-data request with a file as a form part. You can store and read any files from the /tmp directory.

This can be especially helpful for uploading large files: it streams the file from disk, minimizing the memory the workflow uses when uploading the file.

const axios = require("axios");
const fs = require("fs");
const FormData = require("form-data");

const formData = new FormData();
formData.append("file", fs.createReadStream(params.pathToYourFile));
const headers = formData.getHeaders();

const config = {
  method: "POST",
  url: params.url,
  headers,
  data: formData,
};
return await axios(config);
Copy this workflow to run this example.

#Use an HTTP proxy to proxy requests through another host
When you make HTTP requests to certain services, they might require you whitelist a set of IP addresses those requests come from. Often, this is to improve the security of the target service.

By default, HTTP requests made from Pipedream can come from a range of IP addresses. If you need to make requests from a single IP address, you can route traffic through an HTTP proxy:

const axios = require("axios");

let httpsProxyAgent = require("https-proxy-agent");
const agent = new httpsProxyAgent(`http://${user}:${pass}@${host}:${port}`);

const config = {
  method: "GET",
  url,
  httpsAgent: agent,
};

const resp = await axios.request(config);
