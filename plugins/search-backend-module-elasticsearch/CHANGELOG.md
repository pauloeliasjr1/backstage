# @backstage/plugin-search-backend-module-elasticsearch

## 1.0.1

### Patch Changes

- Updated dependencies
  - @backstage/plugin-search-backend-node@1.0.1

## 1.0.1-next.0

### Patch Changes

- Updated dependencies
  - @backstage/plugin-search-backend-node@1.0.1-next.0

## 1.0.0

### Major Changes

- 7bd7d336b2: This package has been promoted to 1.0. Read more about what it means in [New release: Backstage Search 1.0 blog](https://backstage.io/blog/2022/07/19/releasing-backstage-search-1.0)

### Minor Changes

- c5af773757: **BREAKING**: In order to remain interoperable with all currently supported
  deployments of Elasticsearch, this package will now conditionally use either
  the `@elastic/elasticsearch` or `@opensearch-project/opensearch` client when
  communicating with your deployed cluster.

  If you do not rely on types exported from this package, or if you do not make
  use of the `createElasticSearchClientOptions` or `newClient` methods on the
  `ElasticSearchSearchEngine` class, then upgrading to this version should not
  require any further action on your part. Everything will continue to work as it
  always has.

  If you _do_ rely on either of the above methods or any underlying types, some
  changes may be needed to your custom code. A type guard is now exported by this
  package (`isOpenSearchCompatible(options)`), which you may use to help clarify
  which client options are compatible with which client constructors.

  If you are using this package with the `search.elasticsearch.provider` set to
  `aws`, and you are making use of the `newClient` method in particular, you may
  wish to start using the `@opensearch-project/opensearch` client in your custom
  code.

### Patch Changes

- 71de198828: Updated dependency `@opensearch-project/opensearch` to `^2.0.0`.
- b0b8213056: Feature: add a new option to set the batch size for elastic search engine, if not given the default batch size is 1000

  Example usage:

  ```yaml
  search:
    elasticsearch:
      batchSize: 100
  ```

- a21cd43467: Throws `MissingIndexError` when no index of type exist.
- Updated dependencies
  - @backstage/plugin-search-backend-node@1.0.0
  - @backstage/plugin-search-common@1.0.0

## 0.2.0-next.2

### Patch Changes

- 71de198828: Updated dependency `@opensearch-project/opensearch` to `^2.0.0`.
- a21cd43467: Throws `MissingIndexError` when no index of type exist.
- Updated dependencies
  - @backstage/plugin-search-backend-node@0.6.3-next.2

## 0.2.0-next.1

### Minor Changes

- c5af773757: **BREAKING**: In order to remain interoperable with all currently supported
  deployments of Elasticsearch, this package will now conditionally use either
  the `@elastic/elasticsearch` or `@opensearch-project/opensearch` client when
  communicating with your deployed cluster.

  If you do not rely on types exported from this package, or if you do not make
  use of the `createElasticSearchClientOptions` or `newClient` methods on the
  `ElasticSearchSearchEngine` class, then upgrading to this version should not
  require any further action on your part. Everything will continue to work as it
  always has.

  If you _do_ rely on either of the above methods or any underlying types, some
  changes may be needed to your custom code. A type guard is now exported by this
  package (`isOpenSearchCompatible(options)`), which you may use to help clarify
  which client options are compatible with which client constructors.

  If you are using this package with the `search.elasticsearch.provider` set to
  `aws`, and you are making use of the `newClient` method in particular, you may
  wish to start using the `@opensearch-project/opensearch` client in your custom
  code.

### Patch Changes

- Updated dependencies
  - @backstage/plugin-search-backend-node@0.6.3-next.1
  - @backstage/plugin-search-common@0.3.6-next.0

## 0.1.6-next.0

### Patch Changes

- Updated dependencies
  - @backstage/plugin-search-backend-node@0.6.3-next.0

## 0.1.5

### Patch Changes

- 281cec1b61: Use more precise matching for query filters
- 915700f64f: The provided search engine now adds a pagination-aware `rank` value to all results.
- ddce23d080: Now possible to set a custom index template on the elasticsearch search engine.
- 7d8acfc32e: Additional types now exported publicly:

  - ElasticSearchAgentOptions
  - ElasticSearchConcreteQuery
  - ElasticSearchQueryTranslator
  - ElasticSearchConnectionConstructor,
  - ElasticSearchTransportConstructor,
  - ElasticSearchNodeOptions,
  - ElasticSearchOptions,
  - ElasticSearchAuth,

- Updated dependencies
  - @backstage/plugin-search-common@0.3.5
  - @backstage/plugin-search-backend-node@0.6.2

## 0.1.5-next.2

### Patch Changes

- 7d8acfc32e: Additional types now exported publicly:

  - ElasticSearchAgentOptions
  - ElasticSearchConcreteQuery
  - ElasticSearchQueryTranslator
  - ElasticSearchConnectionConstructor,
  - ElasticSearchTransportConstructor,
  - ElasticSearchNodeOptions,
  - ElasticSearchOptions,
  - ElasticSearchAuth,

- Updated dependencies
  - @backstage/plugin-search-common@0.3.5-next.1
  - @backstage/plugin-search-backend-node@0.6.2-next.2

## 0.1.5-next.1

### Patch Changes

- 281cec1b61: Use more precise matching for query filters
- Updated dependencies
  - @backstage/plugin-search-backend-node@0.6.2-next.1
  - @backstage/plugin-search-common@0.3.5-next.0

## 0.1.5-next.0

### Patch Changes

- Updated dependencies
  - @backstage/plugin-search-backend-node@0.6.2-next.0

## 0.1.4

### Patch Changes

- 9eef9c9db4: Fix issue where `nextPageCursor` is defined on the last page of results
- 71d3432710: Search Engines will now index documents in batches of 1000 instead of 100 (under the hood). This may result in your Backstage backend consuming slightly more memory during index runs, but should dramatically improve indexing performance for large document sets.
- a7f7a63d14: Prevent orphaned stale indices by permanently marking them for deletion so removal can be re-attempted if it failed previously
- 3a74e203a8: Support generating highlighted matched terms in search result data
- Updated dependencies
  - @backstage/config@1.0.1
  - @backstage/plugin-search-backend-node@0.6.1
  - @backstage/plugin-search-common@0.3.4

## 0.1.4-next.1

### Patch Changes

- 71d3432710: Search Engines will now index documents in batches of 1000 instead of 100 (under the hood). This may result in your Backstage backend consuming slightly more memory during index runs, but should dramatically improve indexing performance for large document sets.
- 3a74e203a8: Support generating highlighted matched terms in search result data
- Updated dependencies
  - @backstage/config@1.0.1-next.0
  - @backstage/plugin-search-backend-node@0.6.1-next.1
  - @backstage/plugin-search-common@0.3.4-next.0

## 0.1.4-next.0

### Patch Changes

- a7f7a63d14: Prevent orphaned stale indices by permanently marking them for deletion so removal can be re-attempted if it failed previously
- Updated dependencies
  - @backstage/plugin-search-backend-node@0.6.1-next.0

## 0.1.3

### Patch Changes

- 62ee65422c: Use new `IndexableResultSet` type as return type of query method in `SearchEngine` implementation.
- Updated dependencies
  - @backstage/plugin-search-common@0.3.3
  - @backstage/plugin-search-backend-node@0.6.0

## 0.1.3-next.1

### Patch Changes

- Updated dependencies
  - @backstage/plugin-search-backend-node@0.6.0-next.1

## 0.1.3-next.0

### Patch Changes

- 62ee65422c: Use new `IndexableResultSet` type as return type of query method in `SearchEngine` implementation.
- Updated dependencies
  - @backstage/plugin-search-common@0.3.3-next.0
  - @backstage/plugin-search-backend-node@0.5.3-next.0

## 0.1.2

### Patch Changes

- Updated dependencies
  - @backstage/config@1.0.0
  - @backstage/plugin-search-backend-node@0.5.2
  - @backstage/plugin-search-common@0.3.2

## 0.1.1

### Patch Changes

- 3e54f6c436: Use `@backstage/plugin-search-common` package instead of `@backstage/search-common`.
- Updated dependencies
  - @backstage/plugin-search-common@0.3.1
  - @backstage/plugin-search-backend-node@0.5.1

## 0.1.1-next.0

### Patch Changes

- 3e54f6c436: Use `@backstage/plugin-search-common` package instead of `@backstage/search-common`.
- Updated dependencies
  - @backstage/plugin-search-common@0.3.1-next.0
  - @backstage/plugin-search-backend-node@0.5.1-next.0

## 0.1.0

### Minor Changes

- 022507c860: **BREAKING**

  The `ElasticSearchSearchEngine` implements the new stream-based indexing
  process expected by the latest `@backstage/plugin-search-backend-node`.

  When updating to this version, you must also update to the latest version of
  `@backstage/plugin-search-backend-node`. Check [this upgrade guide](https://backstage.io/docs/features/search/how-to-guides#how-to-migrate-from-search-alpha-to-beta)
  for further details.

### Patch Changes

- Updated dependencies
  - @backstage/plugin-search-backend-node@0.5.0
  - @backstage/search-common@0.3.0

## 0.0.10

### Patch Changes

- Fix for the previous release with missing type declarations.
- Updated dependencies
  - @backstage/config@0.1.15
  - @backstage/search-common@0.2.4

## 0.0.9

### Patch Changes

- c77c5c7eb6: Added `backstage.role` to `package.json`
- 4c0332e55c: chore(deps-dev): bump `@elastic/elasticsearch-mock` from 0.3.0 to 1.0.0
- Updated dependencies
  - @backstage/config@0.1.14
  - @backstage/search-common@0.2.3

## 0.0.8

### Patch Changes

- Updated dependencies
  - @backstage/config@0.1.13

## 0.0.8-next.0

### Patch Changes

- Updated dependencies
  - @backstage/config@0.1.13-next.0

## 0.0.7

### Patch Changes

- 68512f5178: Add `newClient()` method to re-use the configuration of the elastic search
  engine with custom clients

## 0.0.6

### Patch Changes

- dcd1a0c3f4: Minor improvement to the API reports, by not unpacking arguments directly

## 0.0.5

### Patch Changes

- 36350bf8b3: Pinning version of elastic search client to 7.13.0 to prevent breaking change towards third party ElasticSearch clusters on 7.14.0.

## 0.0.4

### Patch Changes

- f0c2c81676: Added rejectUnauthorized config option

## 0.0.3

### Patch Changes

- a13f21cdc: Implement optional `pageCursor` based paging in search.

  To use paging in your app, add a `<SearchResultPager />` to your
  `SearchPage.tsx`.

- Updated dependencies
  - @backstage/search-common@0.2.0

## 0.0.2

### Patch Changes

- 76872096b: Fix to allow optionally reading `auth` parameter for custom hosted ElasticSearch instances. Also remove `bearer` auth config since it's currently unsupported.
