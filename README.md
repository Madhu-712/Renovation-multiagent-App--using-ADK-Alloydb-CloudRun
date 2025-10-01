# Renovation Agent

This project is a multi-agent system for kitchen renovation using Vertex AI ADK and Gemini 2.5. It has three agents: Renovation Proposal Agent, Permits and Compliance Check Agent, and Order Status Check Agent.

This project is based on the Google Codelab: [Multi-agent App with ADK, Agent Engine and AlloyDB](https://codelabs.developers.google.com/multi-agent-app-with-adk).

## Prerequisites

- A Google Cloud Project with billing enabled.
- [Google Cloud SDK](https://cloud.google.com/sdk/docs/install) installed and configured.
- Python 3.9+

## Setup

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/Madhu-712/renovation-agent.git
    cd renovation-agent
    ```

2.  **Enable Google Cloud services:**
    ```bash
    gcloud services enable artifactregistry.googleapis.com cloudbuild.googleapis.com run.googleapis.com aiplatform.googleapis.com
    ```

3.  **Create and activate a virtual environment:**
    ```bash
    python3 -m venv .venv
    source .venv/bin/activate
    ```

4.  **Install ADK and other dependencies:**
    ```bash
    pip install google-adk
    pip install -r requirements.txt
    ```

5.  **Create a Cloud Storage Bucket:**
    Create a Cloud Storage bucket and make it public.

6.  **Set up AlloyDB:**
    - Create an AlloyDB cluster and instance.
    - Create the `material_order_status` table using the `database_script.sql` file.
    - Insert data into the table.

7.  **Create a Cloud Run Function:**
    - Create a Cloud Run function in Java to extract order status information.
    - Use the code from the `Cloud Run Function` directory in the [original repository](https://github.com/AbiramiSukumaran/adk-renovation-agent).

8.  **Set up Environment Variables:**
    Create a `.env` file and add the following variables:
    ```
    GOOGLE_API_KEY=<YOUR_GOOGLE_API_KEY>
    STORAGE_BUCKET=<YOUR_STORAGE_BUCKET>
    GOOGLE_CLOUD_PROJECT=<YOUR_GOOGLE_CLOUD_PROJECT>
    GOOGLE_CLOUD_LOCATION=<YOUR_GOOGLE_CLOUD_LOCATION>
    GOOGLE_GENAI_USE_VERTEXAI=True
    CHECK_ORDER_STATUS_ENDPOINT=<YOUR_CLOUD_RUN_FUNCTION_URL>
    ```

## Execution

1.  **Run the agent in the terminal:**
    ```bash
    adk run .
    ```

2.  **Run the agent with a web UI:**
    ```bash
    adk web
    ```

## Deployment

-   **To Cloud Run:**
    ```bash
    adk deploy cloud_run --project=<YOUR_PROJECT_ID> --region=us-central1 --service_name=renovation-agent --app_name=renovation-app --with_ui ./renovation-agent
    ```

-   **To Agent Engine:**
    ```bash
    adk deploy agent_engine --project <YOUR_PROJECT_ID> --region us-central1 --staging_bucket gs://<YOUR_BUCKET_NAME> --trace_to_cloud renovation-agent
    ```