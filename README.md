github-review-stats
===================

Get statistics about GitHub code reviews. Fetch data from GitHub and generate a
graph showing the number of days it takes for pull requests to be reviewed.


## Usage

	$ ./github-review-stats-run <GITHUB_TOKEN> 2024-08-31 <OWNER/REPO>

A bar graph will be generated at <REPO>.png showing the count of pull requests
by the number of days taken until their first review.

For example, running the following command on 2024-09-09:

	$ ./github-review-stats-run <GITHUB_TOKEN> 2024-08-01 qmk/qmk_firmware

with the following patch applied:

``` patch
diff --git a/github-review-stats b/github-review-stats
index 09c0752..29a1e01 100644
--- a/github-review-stats
+++ b/github-review-stats
@@ -78,10 +78,13 @@ def plot_graph(pull_requests_file, days_to_first_review):
         matplotlib.ticker.FixedLocator(range(0, max(num_days) + 1)),
     )
     axes.yaxis.set_major_locator(
-        matplotlib.ticker.MultipleLocator(),
+        matplotlib.ticker.MultipleLocator(base=2),
+    )
+    axes.yaxis.set_minor_locator(
+        matplotlib.ticker.AutoMinorLocator(n=2),
     )
 
-    axes.set_title(graph_title)
+    axes.set_title(graph_title + ' (2024-08-01 – 2024-09-09)')
     axes.set_xlabel('Days until first review')
     axes.set_ylabel('Count of pull requests')
 
```

produces the following graph:

![Graph showing the count of pull requests in the qmk/qmk_firmware repository
grouped by number of days until the first code review between 2024-08-01 and
2024-09-09](./Example.png)


## Install

	$ git clone https://github.com/teddywing/github-review-stats.git
	$ cd github-review-stats/
	$ python3 -m venv venv
	$ . venv/bin/activate
	$ pip install -r requirements.txt


## Ideas
* Plot addition and deletion count against days to first review (requires
  GraphQL API or a local copy of the repository).


## Bugs
* github-fetch-reviews: Frequently errors with “OSError: [Errno 12] Cannot
  allocate memory”. To bypass the error, keep re-running the script until it
  completes successfully.


## License
Copyright © 2024 Teddy Wing. Licensed under the GNU GPLv3+ (see the included
COPYING file).
