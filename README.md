# unitvectory-labs-badgeindexer

[badgeindexer](https://github.com/UnitVectorY-Labs/badgeindexer) for [UnitVectorY-Labs](https://github.com/UnitVectorY-Labs)

The [crawl workflow](.github/workflows/badgeindexer-crawl.yml) refreshes badge data every Saturday at 21:00 UTC and supports manual dispatch. Successful push CI on `badgeindexer`'s `main` also starts a crawl through the organization's ghook4action routing configuration. Crawls build current tool `main`, commit data to this repository's `main`, and run serially to avoid overlapping data pushes. The source revision can be newer than the CI run that requested the crawl.

The [generator workflow](.github/workflows/badgeindexer-generate.yml) publishes Pages after a successful crawl on this repository's `main`, on pushes to `main`, or on manual dispatch. It reads current `main` so crawl completion includes the newly committed data. Generation builds current tool `main`. Failed crawls do not start completion-triggered publication. Repeated dispatches can repeat crawls and publication; concurrency does not deduplicate them.
