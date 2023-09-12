# wrangler-mac-bug
This is a repo dedicated to quickly replicate a bug with wrangler 3.x on Apple ARM (M1 or M2). The web server is serving roughly 1MB of content and stopping, no matter what the content size of the file is. I don't have insight if this is a race condition relative to the speed of serving the content or a content size limit. Text based content such as JS is signficnatly more failure prone as it doesn't retry in the browser.

This test will only fail on Mac ARM based processors. It has been replicated on a M1 Air and M2 Pro, but is not replicatable on a Windows machine.

## Results

Run `npm run dev` on the Mac. Open the browser to see a page like this:

![Initial progress screenshot](/screenshots/initial.png)

This run took 5 minutes to serve a basic 24MB image! The browser retried this content to eventually serve the full amount.

![Loaded results taking 5 minutes screenshot](/screenshots/retries.png)

In most cases the browser gives up and sends a content mismatch error:

![Error results screenshot](/screenshots/retries.png)
