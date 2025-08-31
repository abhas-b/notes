#aws [[My Blogs]]

* Basic way of infra management: Manual, using console
	* issues:
		* Error prone
		* Not reproducible in different environments
		* Manual intervention required
		* time consuming
* Alternate:
	* write shell script with all required services and their scripts being managed by CI/CD.
	* Issues:
		* No retry logic
		* no rollbacks
		* No updates
		* 