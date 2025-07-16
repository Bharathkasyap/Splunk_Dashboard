### Sample SPL Queries:
```spl
sourcetype=access_combined_wcookie | top categoryId
sourcetype=access_combined_wcookie | stats count by clientip
sourcetype=linux_secure | stats count by src, user
```
