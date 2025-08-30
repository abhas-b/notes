#aws  [[AWS]]

1. How do you ensure data integrity and quality in a pipeline
	1. Validation checks such as schema validation, constraint checks.
	2. Data audits for metrics to assess quality such as completeness, accuracy and consistency.
2. How do you handle encryption?
	1. Data at rest: SSE
	2. Data in transit: TLS (Transport Layer Security)
3. About your project, can you mention the architecture like what was the source, transformations, sink etc.
	1. Source: Oracle database
	2. Use DMS
	3. Redshift for DWH for fact and dimension tables.
	4. Using stored procedure and external tables using Redshift and spectrum to get the CDC data.
4. How much is the data load using DMS?
	1. We have enabled CDC in DMS. Whenever there is a transaction it will write it in log (write ahead log).
5. If you have a recon process there is a data discrepancy  due to a corrupt record how would you handle it?
	1. if its a job failure, then we can check cloud watch metrics for the step function.
	2. In case of a KPI mismatch we can go to the specific fact table and track its lineage for that metric.
6. What are different measures for securing your S3 bucket?
	1. IAM permissions
	2. bucket policy
	3. Lakehouse
7. How will you handle PII information?
	1. Mask the data
8. What is the difference between db sharding and partitioning?
9. For a pipeline how would you ensure logging and data lineage are in place?
10. How are you deploying your pipeline?
11. Can Athena detect partitions automatically or do you need a command?
12. What are the key components of S3?
	1. Bucket name
	2. Key: unique identifier in a bucket
	3. Objects
		1. Data
		2. Metadata
	4. Encryption
	5. Bucket policy