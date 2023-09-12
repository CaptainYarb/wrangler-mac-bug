# wrangler-mac-bug
This is a repo dedicated to quickly replicate a bug with wrangler 3.x on Apple ARM (M1 or M2). The web server is serving roughly 1MB of content and stopping, no matter what the content size of the file is. I don't have insight if this is a race condition relative to the speed of serving the content or a content size limit. Text based content such as JS is signficnatly more failure prone as it doesn't retry in the browser.

This test will only fail on Mac ARM based processors. It has been replicated on a M1 Air and M2 Pro, but is not replicatable on a Windows machine.

## Results

Run `npm run dev` on the Mac. Open the browser to see a page like this:

![screenshots/initial.png](Initial Progress)

This run took 5 minutes to serve a basic 24MB image! The browser retried this content to eventually serve the full amount.

![screenshots/retries.png](Loaded Result)

In most cases the browser gives up and sends a content mismatch error:

![screenshots/retries.png](Loaded Result)

When on Wrangler v2.x this bug is not present:

![screenshots/wrangler-v2-success.png](Successful result on wrangler v2.x)