### GremliNPM

A basic search tool for NPM.

### Planning

- The search bar is omnipresent
- Could either use a route to show /results, or a state {results} conditional flag
- At first, the page is simply a search field in a fixed top bar
- As a user types, requests are sent to the API
  - need to Debounce this - if a request is in progress, don't send new requests
- The only interaction button is the 'search' button; when clicked, a request is sent to `https://api.npms.io/v2/search/suggestions?q=${queryString}` where queryString is the current value of the form input.
- Once results come back, they are shown in a (paginated? maybe if time allows...) list

  - the data is JSON API spec, comes back in this format:

  ```
  [
    {
      package: {
        name, description, ... , date, author
      },
      score: {...},
      searchScore: INT,
      highlight: STRING,

    }
  ]
  ```

  - the list doesn't always come back in order; sort by search-score
  - each list item will need a title, description, and be wrapped in a link
  - for E.C., show UI that indicates exact match, and also npm score

### Architecture

- Redux for state management
- Thunks for async handling of the NPM requests
- React-Router for showing /results. Using a route instead of a state flag in preparation for a possible pagination feature (would require query-params)
- Will use css/sass at first, then re-implement with Emotion just for kicks if there is time
- Responsive design
- Fail states & testing
