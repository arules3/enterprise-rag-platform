# enterprise-rag-platform

1) Documents are stored in GCS to harness the security and durable object storage provided by Google to store unstructured data . Furthermore , GCS is comparably less costlier     than its cloud counterparts which will help us to minimize the storage cost .
2) Querying the Pdf's directly will make our ingestion pipeline slower resulting in computing and ingesting the stored data every time when we are going to run our ingestion       function or pipeline .
3) In this project Delta Lake will solve the problem of storing post analytical data and keeping different versions of it to perform different analysis later based upon the        requirement .
4) Auto loader service will help us to identify new uploaded files and only perform uploading actions for the newer files ignoring the files that are already stored on GCS.
5) Embedding are required to make the data more semantically meaningful for the LLM to understand it and querying it more efficiently using chunking , overlap and other            semantic text based splitter techniques .
6) Vector Search is required to query the data and give desired output from the embeddings data stored in vector database . As data will be stored in Vector DB to utilize the      cosine similarity based vector based search which will result in more precise output of the user's queries .
7) FastApi will provide us all the tools and functions required to become the intermediate to send and receive user's queries . It provides various useful tools and strategies     that would be helpful to pre-process the query and post process the response data to make it more secure and readable to maintain data cleanliness .



<h1>GCS → Delta → Vector Search </h1>
<p1> is primarily our data/indexing pipeline. </p1>

<h1>FastAPI → Vector Search → LLM</h1>
<p1> is our online serving pipeline. </p1>

<h1>MLflow → GitHub Actions</h1>
<p1> is our quality/CI pipeline. </p1>


                   ** RAW DATA
                       │
                       ▼
                     GCS
              "Where files live"
                       │
                       │ Auto Loader
                       ▼
                 DELTA LAKE
            "Reliable data layer"
                       │
                       │ Sync
                       ▼
               VECTOR SEARCH
             "Retrieval layer"
                       │
                       │ relevant chunks
                       ▼
                    FASTAPI
              "Application/API"
                       │
                       ▼
                     LLM
              "Generate answer"
                       │
                       ▼
                   Response


             ───── QUALITY LAYER ─────

                 MLflow Evaluation
                       │
                       ▼
                GitHub Actions
                       │
                       ▼
                 Quality Gates**
