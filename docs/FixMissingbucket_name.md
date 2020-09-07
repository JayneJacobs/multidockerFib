Fix for Missing bucket_name error
The dpl script Travis uses to deploy and do build verification is currently broken for many students. If you are getting a persistent missing bucket_name error with a failed build you will need to add the following to your .travis.yml file:

```
deploy:
  edge: true
  provider: elasticbeanstalk
  ...
```

What this is doing is forcing Travis to use the v2 (experimental) version of the dpl script which does not have the bug.

 
