# jenkinstriggercommitmsg
This pipeline first checks out your Git repository and retrieves the commit message of the latest commit.
It then checks if the commit message contains the keyword [TEST-123].
If the keyword is present, the pipeline proceeds to the 'Your Job' stage, where you can add your specific job steps. 
If the keyword is not present, the pipeline will be aborted.