project_path: /web/_project.yaml
book_path: /web/_book.yaml
description: Add JavaScript to install a service worker

A completed version of this step is in the completed/step3 directory.



## 1. Create index.html

In your _app_ directory, create the file _index.html_ and add the following
code:

<div class="highlight"><pre><code class="language-html" data-lang="html"><span class="cp">&lt;!DOCTYPE html&gt;</span>
<span class="nt">&lt;html&gt;</span>
<span class="nt">&lt;head&gt;</span>
  <span class="nt">&lt;title&gt;</span>Push Notification codelab<span class="nt">&lt;/title&gt;</span>
<span class="nt">&lt;/head&gt;</span>
<span class="nt">&lt;body&gt;</span>
  <span class="nt">&lt;h1&gt;</span>Push Notification codelab<span class="nt">&lt;/h1&gt;</span>
  <span class="nt">&lt;p&gt;</span>This page must be accessed using HTTPS or via localhost.<span class="nt">&lt;/p&gt;</span>
  <span class="nt">&lt;script </span><span class="na">src=</span><span class="s">&quot;js/main.js&quot;</span><span class="nt">&gt;&lt;/script&gt;</span>
<span class="nt">&lt;/body&gt;</span>
<span class="nt">&lt;/html&gt;</span></code></pre></div>

Open _index.html_ locally in Chrome from localhost: the URL should be something like _http://localhost/push-notifications/app/index.html_.

## 2. Add a Service Worker

In your _app_ directory, create an empty file named _sw.js_. You'll add code
to this later.

Don't worry if you haven't used service workers before. You won't need to know much about them to complete this codelab. Service workers are worker scripts that run in the background to intercept network requests, handle push messages and perform other tasks. If you want to find out more, take a look at [Introduction to Service Worker](http://www.html5rocks.com/en/tutorials/service-worker/introduction/) on HTML5 Rocks.

When a push message is received, the browser can run a service worker in the background to handle push messages without requiring a web page to be open.

## 3. Register and install a Service Worker

In this step you create the _main.js_ JavaScript file referred to in
_index.html_. This in turn gives access to the service worker script.  In your _app_ directory, create a _js_ directory and add to it a file named
_main.js_ with the following code:

<div class="highlight"><pre><code class="language-javascript" data-lang="javascript"><span class="k">if</span> <span class="p">(</span><span class="s1">&#39;serviceWorker&#39;</span> <span class="k">in</span> <span class="nx">navigator</span><span class="p">)</span> <span class="p">{</span>
 <span class="nx">console</span><span class="p">.</span><span class="nx">log</span><span class="p">(</span><span class="s1">&#39;Service Worker is supported&#39;</span><span class="p">);</span>
 <span class="nx">navigator</span><span class="p">.</span><span class="nx">serviceWorker</span><span class="p">.</span><span class="nx">register</span><span class="p">(</span><span class="s1">&#39;sw.js&#39;</span><span class="p">).</span><span class="nx">then</span><span class="p">(</span><span class="kd">function</span><span class="p">(</span><span class="nx">reg</span><span class="p">)</span> <span class="p">{</span>
   <span class="nx">console</span><span class="p">.</span><span class="nx">log</span><span class="p">(</span><span class="s1">&#39;:^)&#39;</span><span class="p">,</span> <span class="nx">reg</span><span class="p">);</span>
   <span class="c1">// TODO</span>
 <span class="p">}).</span><span class="k">catch</span><span class="p">(</span><span class="kd">function</span><span class="p">(</span><span class="nx">err</span><span class="p">)</span> <span class="p">{</span>
   <span class="nx">console</span><span class="p">.</span><span class="nx">log</span><span class="p">(</span><span class="s1">&#39;:^(&#39;</span><span class="p">,</span> <span class="nx">err</span><span class="p">);</span>
 <span class="p">});</span>
<span class="p">}</span></code></pre></div>

This code checks if service worker is supported by your browser, then registers and installs the service worker you created in _sw.js_ — which doesn't do anything (yet!)

## 4. Try it out from localhost

Open _index.html_ from localhost and open Chrome DevTools to check the
console.

It should look like this:

<img src="images/image01.png" width="965" height="901" alt="Codelab web page open in Chrome, showing ServiceWorkerRegistration in DevTools console" />

## 5. Try out serviceworker-internals

The diagnostic page _chrome://serviceworker-internals_ is a good place to
check that your service workers are working:

<img src="images/image02.png" width="907" height="641" alt="chrome:serviceworker-internals diagnostic page open in Chrome" />

## 6. Add event listeners to your Service Worker

Add the following code to _sw.js_:

<div class="highlight"><pre><code class="language-javascript" data-lang="javascript"><span class="nx">console</span><span class="p">.</span><span class="nx">log</span><span class="p">(</span><span class="s1">&#39;Started&#39;</span><span class="p">,</span> <span class="nx">self</span><span class="p">);</span>
<span class="nx">self</span><span class="p">.</span><span class="nx">addEventListener</span><span class="p">(</span><span class="s1">&#39;install&#39;</span><span class="p">,</span> <span class="kd">function</span><span class="p">(</span><span class="nx">event</span><span class="p">)</span> <span class="p">{</span>
  <span class="nx">self</span><span class="p">.</span><span class="nx">skipWaiting</span><span class="p">();</span>
  <span class="nx">console</span><span class="p">.</span><span class="nx">log</span><span class="p">(</span><span class="s1">&#39;Installed&#39;</span><span class="p">,</span> <span class="nx">event</span><span class="p">);</span>
<span class="p">});</span>
<span class="nx">self</span><span class="p">.</span><span class="nx">addEventListener</span><span class="p">(</span><span class="s1">&#39;activate&#39;</span><span class="p">,</span> <span class="kd">function</span><span class="p">(</span><span class="nx">event</span><span class="p">)</span> <span class="p">{</span>
  <span class="nx">console</span><span class="p">.</span><span class="nx">log</span><span class="p">(</span><span class="s1">&#39;Activated&#39;</span><span class="p">,</span> <span class="nx">event</span><span class="p">);</span>
<span class="p">});</span>
<span class="nx">self</span><span class="p">.</span><span class="nx">addEventListener</span><span class="p">(</span><span class="s1">&#39;push&#39;</span><span class="p">,</span> <span class="kd">function</span><span class="p">(</span><span class="nx">event</span><span class="p">)</span> <span class="p">{</span>
  <span class="nx">console</span><span class="p">.</span><span class="nx">log</span><span class="p">(</span><span class="s1">&#39;Push message received&#39;</span><span class="p">,</span> <span class="nx">event</span><span class="p">);</span>
  <span class="c1">// TODO</span>
<span class="p">});</span></code></pre></div>

In a service worker, `self` refers to the `ServiceWorkerGlobalScope` object: the service worker itself.

**TOP TIP!**

By default an old service worker will stay running until all tabs that use it are closed or unloaded. A new service worker will remain in the `waiting` state.

When `skipWaiting()` is called (as in the code above) the service worker will skip the waiting state and immediately activate.

Handy for debugging!

Click the **Inspect** button on the _chrome://serviceworker-internals_ page. You should see the following:

<img src="images/image03.png" width="888" height="845" alt="Chrome DevTools console showing service worker instal and activate events" />

**Warning**: If there are errors parsing your service worker code, it won't be installed and an error will be thrown during the install event.
This can result in a service worker mysteriously not updating when you change the code. Always remember to check and validate your code when you change it!

