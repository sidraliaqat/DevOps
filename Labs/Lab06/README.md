# Lab 6: Nexus Repository Setup and User Access

## What was done

| Task | Work | Screenshots |
|------|------|-------------|
| 1 | Ran Nexus in Docker (ports 8006 and 8007, volume `nexus-data`), set admin password, disabled anonymous access | `nexus_container_running.png` |
| 2 | Created role `nx-java` (maven-snapshots privilege) and user `nexus`, verified with the Status API (HTTP 200) | `nexus_user_access.png` |
| 3 | Configured the Gradle project `my-app`, built the JAR and published it to `maven-snapshots` | `gradle_nexus_configuration.png`, `gradle_nexus_build.png`, `gradle_nexus_publish.png`, `nexus_gradle_artifact.png` |
| 4 | Added `distributionManagement` to `java-maven-app`, ran `mvn package` and `mvn deploy` | `maven_nexus_project.png`, `maven_distribution_management.png`, `maven_package_nexus.png`, `maven_deploy_nexus.png`, `nexus_maven_artifact.png` |
| 5 | Queried repositories (as `nexus` and `admin`), listed components and fetched one by ID through the REST API | `nexus_repositories_user.png`, `nexus_repositories_admin.png`, `nexus_components_list.png`, `nexus_component_details.png` |
| 6 | Inspected the default blob store, created `mystore`, created the `docker-hosted` repository on port 8007 | `nexus_default_blob_content.png`, `nexus_mystore_created.png`, `nexus_blob_directories.png`, `nexus_docker_hosted_repository.png` |
| 7 | Created the `maven` cleanup policy, ran the cleanup service, then compacted the default blob store | `nexus_cleanup_policy_created.png`, `nexus_cleanup_policy_attached.png`, `nexus_cleanup_task_waiting.png`, `nexus_cleanup_task_completed.png`, `nexus_maven_snapshots_empty.png`, `nexus_blob_store_before_compaction.png`, `nexus_compact_task_configured.png`, `nexus_compact_task_completed.png`, `nexus_blob_store_after_compaction.png` |

## Compaction result (default blob store)

| | Before | After |
|---|---|---|
| Blob count | 112 | 40 |
| Used size | 158.58 MB | 805.13 kB |
| Available space | 18.16 GB | 18.32 GB |

## Notes

- Nexus ran directly on the Ubuntu server. Gradle and Maven ran in the IntelliJ container.
- Credentials are kept out of the repository: `gradle.properties` and `~/.m2/settings.xml` are not committed.
- `curl -u <user>` was used without a password on the command line, so curl prompted for it.
- The `nexus` container and `nexus-data` volume are kept for the next lab.

## Files

- `screenshots/` has all 28 required screenshots
- `Lab6_Solution.pdf` has the evidence in task order
