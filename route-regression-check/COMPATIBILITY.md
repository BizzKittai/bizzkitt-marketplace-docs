# Compatibility and verification

Version 1.0.0. Native validation on 11 November 2026: Unity 6000.3.28f1 (6.3 LTS), macOS ARM64, Unity Test Framework 1.6.0. All 44 distinct Edit Mode cases passed, including native NavMesh baking/querying, invalid input, stale reports, area costs and link changes. The visible Editor demonstrated three passes, an intentional length failure and stale-result export invalidation. A real local JSON file was exported through the native save dialog. A separate blank project successfully imported the native package and ran both included example suites.

The checker uses UnityEngine.AI and UnityEditor APIs with no third-party package dependency. The optional demo is authored with URP 17.3.0 and uses Unity standard primitives plus included baked navigation. The example component only registers its own NavMeshData while enabled. Unity Pipeline is development infrastructure and is excluded from the distribution.

The tool targets Unity 6000.3 LTS. Only the stated patch and operating system have been tested. Windows, Linux, earlier Unity versions, customer projects and runtime character traversal have not been tested. The core checks do not depend on a render pipeline; the supplied demo materials require URP. A native package export/import acceptance receipt is tracked outside the package to avoid a self-referential hash.

Local validation is not Asset Store approval or a promise of fault-free operation. Review the limitations in [Quick start](QUICKSTART.md) before use.
