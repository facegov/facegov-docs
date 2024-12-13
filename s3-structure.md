# S3 Structure

Facegov bucket and folder structure:

1. Main Website Bucket (facegov.com):
   * Purpose: Hosts your static website files
   * Structure:
     * /index.html and other HTML files at root
     * /assets/css/ for stylesheets
     * /assets/js/ for JavaScript files
     * /assets/images/ for website images
2. Data Bucket (data.facegov.com):
   * Purpose: Stores application data and ML models
   * Structure:
     * /requests/
       * /raw/ - Initial user queries
       * /processed/ - Preprocessed queries ready for ML
     * /responses/
       * /raw/ - Initial system responses
       * /processed/ - Post-processed responses with analytics
     * /models/
       * /current/ - Active SageMaker models
       * /archive/ - Previous model versions
     * /training-data/
       * /conversations/ - Historical Q\&A pairs
       * /embeddings/ - Processed embeddings for ML
3. Logs Bucket (logs.facegov.com):
   * Purpose: Stores various system logs
   * Structure:
     * /access-logs/ - Website access logs
     * /application-logs/ - Backend service logs
     * /error-logs/ - System error logs

Recommendations for implementation:

1. Bucket Policies:
   * facegov.com: Public read access for website hosting
   * data.facegov.com: Private, accessed only by backend services
   * logs.facegov.com: Private, accessed only by logging services
2. File Organization:
   * Use ISO date prefixes for logs: YYYY/MM/DD/
   * Use UUID or timestamp-based naming for request/response files
   * Keep current model separate from archived versions
3. Lifecycle Rules:
   * Move older logs to cheaper storage classes after 30 days
   * Archive training data older than 90 days to Glacier
   * Keep only last 5 versions of archived models
