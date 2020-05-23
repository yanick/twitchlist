
## Install

    $ npm install
    $ npm run start

    // go and check localhost:8080

Don't forget to populate the right client-id and auth token
in `src/App.svelte`.

## Notes

To be able to reach the twitch api without CORS pains, 
I've configured the webpack dev server to proxy calls 
to the route `/api/*`. If the app is deployed to a server,
the final deployment will have to do the same kind of proxying.

