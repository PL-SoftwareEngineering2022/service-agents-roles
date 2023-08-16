locals {
  service_agents_policy = {
    "roles/artifactregistry.serviceAgent"  = ["serviceAccount:service-${data.google_project.project.number}@gcp-sa-artifactregistry.iam.gserviceaccount.com"],
    "roles/cloudbuild.serviceAgent"        = ["serviceAccount:service-${data.google_project.project.number}@gcp-sa-cloudbuild.iam.gserviceaccount.com"],
    "roles/cloudfunctions.serviceAgent"    = ["serviceAccount:service-${data.google_project.project.number}@gcf-admin-robot.iam.gserviceaccount.com"],
    "roles/compute.serviceAgent"           = ["serviceAccount:service-${data.google_project.project.number}@compute-system.iam.gserviceaccount.com"],
    "roles/container.serviceAgent"         = ["serviceAccount:service-${data.google_project.project.number}@container-engine-robot.iam.gserviceaccount.com"],
    "roles/firestore.serviceAgent"         = ["serviceAccount:service-${data.google_project.project.number}@gcp-sa-firestore.iam.gserviceaccount.com"],
    "roles/cloudkms.serviceAgent"          = ["serviceAccount:service-${data.google_project.project.number}@gcp-sa-cloudkms.iam.gserviceaccount.com"],
    "roles/servicenetworking.serviceAgent" = ["serviceAccount:service-${data.google_project.project.number}@service-networking.iam.gserviceaccount.com"],
    "roles/spanner.serviceAgent"           = ["serviceAccount:service-${data.google_project.project.number}@gcp-sa-spanner.iam.gserviceaccount.com"],
    "roles/cloudsql.serviceAgent"          = ["serviceAccount:service-${data.google_project.project.number}@gcp-sa-cloud-sql.iam.gserviceaccount.com"],
  }
}

data "google_project" "project" {}

resource "google_project_iam_policy" "common_service_agents_policy" {
  project     = var.GCP_PROJECT
  policy_data = data.google_iam_policy.service_agents_policy.policy_data
}

data "google_iam_policy" "service_agents_policy" {
  dynamic "binding" {
    for_each = concat(keys(local.service_agents_policy))
    content {
      members = compact(
        concat(
          lookup(local.service_agents_policy, binding.value, [""])
        )
      )
      role = binding.value
    }
  }
}
