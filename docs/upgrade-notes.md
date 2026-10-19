# Umbraco maintenance and upgrade notes — 2026-10-19

## Changes

- Move Umbraco CMS from 14.2.0 to **17.7.1 (LTS)** and target **.NET 10**.
- Pin MessagePack **3.1.9** and System.Security.Cryptography.Pkcs **10.0.13** to fix advisories inherited from the CMS dependency graph.
- Disable SDK static-asset compression as required by the Umbraco 14-to-15 upgrade guidance.
- Add `Umbraco.Cms.DevelopmentMode.Backoffice` 17.7.1 to preserve the runtime Razor/InMemoryAuto workflow after it moved out of the core CMS package.

## Verification

Verified using .NET SDK **10.0.402**:

- Release build, including Razor view compilation: passed.
- Release publish: passed.
- NuGet vulnerability scan including transitive dependencies: MessagePack and PKCS advisories resolved; the five ImageSharp advisories below remain.

No application startup against the old Azure connection, database migration, or live deployment was performed. Database contents, templates rendered with real content, backoffice login, uSync import, and other runtime workflows remain unverified. Successful compilation/publishing does not establish that the retired site is restored.

## Remaining dependency issue: ImageSharp

The resolved dependency graph still contains `SixLabors.ImageSharp` **3.1.12**, inherited through Umbraco's imaging packages. The current audit reports five advisories:

- GHSA-gwg2-r3hj-4w44
- GHSA-j3p4-wp97-rph4
- GHSA-j9gm-c75j-xc9q
- GHSA-wmxv-xphr-5c9g
- GHSA-jjfr-hcj7-qf5w

An attempted upgrade to ImageSharp **4.1.2** was rejected by its build targets because no Six Labors license key/file was supplied. That attempted reference was removed; no license checks were bypassed and audit warnings were not suppressed. A properly licensed compatible imaging upgrade needs separate integration validation, or a future compatible Umbraco imaging release must address these advisories. The repository is therefore not free of known dependency advisories.

## Running or restoring later

Use a current patched .NET 10 SDK/runtime. Provide your own local database configuration; the retired Azure account is not required for build or publish. To restore old content, obtain a database/media backup or validate a fresh-database import path. Back up any database before first startup with the new CMS because CMS upgrades can migrate its schema and stored data. Regenerate and review typed models after the migrated schema is available.

Existing database configuration and credentials were not modified as part of this maintenance update. Do not treat checked-in historical connection details as reusable deployment credentials.

## References

- [Umbraco October 2026 security patches](https://umbraco.com/blog/security-advisory-october-6-2026-security-patches-for-umbraco-cms-now-available/)
- [Umbraco version-specific upgrade guide](https://docs.umbraco.com/umbraco-cms/17.latest/get-started/upgrading-and-migrating/version-specific)
- [uSync version compatibility](https://docs.jumoo.co.uk/usync/uSync/versions/)
- [MessagePack advisory](https://github.com/advisories/GHSA-qhrr-8q5h-9q3h)
- [PKCS advisory](https://github.com/advisories/GHSA-846f-f764-76mx)
- [ImageSharp advisory](https://github.com/advisories/GHSA-j3p4-wp97-rph4)
