# pepita
Run a Splunk search from Emacs.

_"Pepita": "nugget" in Spanish._


## Table of contents

<!--ts-->

   * [Installation and configuration](#installation-and-configuration)

   * [Manual](#manual)
     * [Interactive functions](#interactive-functions)
     * [Results buffer](#results-buffer)
   * [Roadmap](#roadmap)
<!--te-->

## Installation and configuration

Place pepita.el in your load-path.  Or install from MELPA (coming soon).

The next step would be to use customize for pepita. Not a lot to see so far:

1. **REQUIRED**: Add the Splunk URL _(Notice the trailing /)_:

```elisp
    (setq 'pepita-splunk-url "https://splunk.something.com:8089/services/")
```

2. You can set `pepita-splunk-username` if you don't want to enter your user name on each session

# Manual

The first request to Splunk you will be prompted user/pass and then your credentials will be
cached in memory as long as Emacs is open. I couldn't get session auth to work 
yet (so we don't need to keep credentials around) but it's a feature in the roadmap.

## Interactive functions

* `pepita-new-search`: Prompts for a query text and time range. If called with prefix arg, 
provides the parameters from the last search as starting point.

* `pepita-search-at-point`: Just like the previous function, but use the region, or current
line if region is not active, as query text. If called with prefix args, prepend the last 
search text to the new input.

I keep an org file with some common queries, in those scenarios the second function is really handy.
It's also useful to refine a search from results (highlight the text you want to add to the query and
call with prefix arg).

## Results buffer

The search runs in the background, and the results are displayed in a new buffer, in CSV format.
From that buffer you can use:
* J - to export to JSON
* H - to export to HTML
* ? - to see the parameters used in the query

## Roadmap

* Create a derived mode for the results buffer
* Provide a way to see searches started but not completed
* Get session auth working
* Handle gracefully not having results. (Maybe change the flow to open the results buffer as soon as search starts)
