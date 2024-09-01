github-review-stats
===================

TODO


## Usage

    $ ./github-review-stats-run <GITHUB_TOKEN> 2024-08-31 <OWNER/REPO>

A bar graph will be generated at <REPO>.png showing the count of pull requests
by the number of days taken until their first review.


## Install

    $ git clone https://github.com/teddywing/github-review-stats.git
    $ cd github-review-stats/
    $ python3 -m venv venv
    $ . venv/bin/activate
    $ pip install -r requirements.txt


## Ideas
* Plot addition and deletion count against days to first review (requires
  GraphQL API or a local copy of the repository).


## License
Copyright © 2024 Teddy Wing. Licensed under the GNU GPLv3+ (see the included
COPYING file).
