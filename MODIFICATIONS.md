# Modifications to Grafana Loki

## License Compliance Notice

This document fulfills the modification disclosure requirements of the GNU Affero General Public License v3.0 (AGPL-3.0) under which the upstream Grafana Loki project is licensed.

**Upstream Project:** [Grafana Loki](https://github.com/grafana/loki)  
**Fork Repository:** [EnterpriseDB/loki](https://github.com/EnterpriseDB/loki)  
**License:** AGPL-3.0 (see LICENSE file in upstream repository)

## Overview

This fork of Grafana Loki contains modifications made by EnterpriseDB to support Azure Data Lake Storage Gen2 (hierarchical namespace) functionality. The upstream Loki does not currently support Azure Storage accounts with hierarchical namespaces enabled, which is required for EDB's Azure deployments.

## Modifications Made

### 1. Azure Data Lake Storage Gen2 Support

**Date:** November 21, 2025  
**Author:** Anhui-tqhuang <tianqiu.huang@enterprisedb.com>  
**Commits:**
- `fa71be115` - auto detect data lake gen 2
- `b2b6bef59` - auto detect data lake gen 2

**Files Modified:**
- `pkg/storage/bucket/azure/bucket_client.go`

**Description:**  
Added automatic detection and support for Azure Data Lake Storage Gen2 (ADLS Gen2) with hierarchical namespaces. This modification enables Loki to work with Azure Storage accounts that have hierarchical namespace enabled, which is a requirement for EDB's Azure Kubernetes Service (AKS) deployments.

**Technical Details:**  
The modification switches to using the EnterpriseDB fork of the objstore library that includes support for hierarchical namespace detection. This change is pending upstream merge of [thanos-io/objstore#238](https://github.com/thanos-io/objstore/pull/238).

### 2. Dependency Updates

**Date:** November-December 2025  
**Commits:**
- `53f59874f` - switch to EnterpriseDB/objstore (November 2025)
- `7444b2d8d` - update go mod vendor (November 2025)
- `feea424cb` - update go mod vendor (December 2025)

**Files Modified:**
- `go.mod`
- `go.sum`
- `vendor/` directory)

**Description:**  
Updated Go module dependencies to use the EnterpriseDB fork of the objstore library and refreshed vendored dependencies accordingly.

## Deployment Information

The modified Loki image is used exclusively for Azure AKS deployments where Azure Storage accounts are configured with hierarchical namespaces. 

## Upstream Integration Status

EnterpriseDB intends to migrate back to the upstream Grafana Loki for AKS deployments once the following conditions are met:

1. The objstore library fix ([thanos-io/objstore#238](https://github.com/thanos-io/objstore/pull/238)) is merged upstream
2. Grafana Loki updates its dependency to include the fixed objstore version
3. A stable release of Loki is published with the fix

## Source Code Availability

As required by AGPL-3.0 Section 13, the complete source code for this modified version is available at:

**Repository:** https://github.com/EnterpriseDB/loki  
**Branch:** `main` and `support-azure-data-lake-gen-2`

## Contact Information

**Organization:** EnterpriseDB  
**Repository:** https://github.com/EnterpriseDB/loki

## Modification History

| Date | Version/Commit | Description |
|------|----------------|-------------|
| 2025-11-21 | fa71be115 | Initial Azure Data Lake Gen2 support |
| 2025-11-21 | 53f59874f | Switch to EnterpriseDB/objstore fork |
| 2025-12-07 | feea424cb | Update vendored dependencies |

---

*This document was last updated: December 8, 2025*
