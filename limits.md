---

copyright:
  years:  2022, 2023, 2024
lastupdated: "2024-04-10"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}

# Limits
{: #limits}

Learn about known limits for {{site.data.keyword.metrics_router_full_notm}}.
{: shortdesc}

## Targets
{: #limits-targets}

* You can define a target in any of the supported locations where {{site.data.keyword.metrics_router_full_notm}} is available. For more information, see [Locations](/docs/metrics-router?topic=metrics-router-regions).

* You can configure up to 16 targets in each account.

* You can configure up to two default targets for each {{site.data.keyword.cloud_notm}} account.

* The target name must be 1000 characters or less and cannot include any special characters other than space, dash `-`, dot `.`, underscore `_`, and colon `:`.

    The name must not include any personal identifying information (PII).
    {: important}

* You can update the name of a target or the CRN of the target resource. The change can take up to 10 minutes to complete.


## Routes
{: #limits-routes}

* You can define a route in any of the supported locations where {{site.data.keyword.metrics_router_full_notm}} is available. For more information, see [Locations](/docs/metrics-router?topic=metrics-router-regions).

* You can define up to 30 routes for an account.

* By default, the account has 0 routes configured.

* You can configure up to 10 rules for each route.

* You can configure up to 3 targets for each rule.

* The route name must be 1000 characters or less and cannot include any special characters other than space, dash `-`, dot `.`, underscore `_`, and colon `:`.

    The name must not include any personal identifying information (PII).
    {: important}

### Inclusion filters
{: #limits-incl-filters}

* You can configure up to 7 inclusion filters for each rule.

* You can configure up to 20 values for `inclusion_filter.values`.

* Each value configured for `inclusion_filter.values` can be a maximum of 100 characters.
