A set of comment data tests for aidanhs/emsnudown.

Originally obtained from [here](http://www.reddit.com/r/redditdev/comments/1h1wqu/anonymous_ftp_access_for_reddit_comment_data_is/) until it was [removed](http://www.reddit.com/r/redditdev/comments/1ji0ta/bulk_reddit_data_available_on_my_ftp_server/cbevn8x).

New comments may be obtained with the [comment stream](http://www.reddit.com/r/TheoryOfReddit/comments/1l0ym4/comment_stream_api_is_up_and_running_feel_free_to/).

Anonymisation has been performed with

```
$ mv 2013-06-27_HOUR-21 2013-06-27_HOUR-21_full
$ python
>>> import json
>>> comments = open("2013-06-27_HOUR-21_full").readlines()
>>> comments = map(lambda x: json.loads(x), comments)
>>> comments = map(lambda x: {u"body": x["body"]}, comments)
>>> out = open("2013-06-27_HOUR-21_stripped", "w")
>>> out.writelines(map(lambda x: json.dumps(x) + "\n", comments))
>>> out.close()
>>>
>>> import re
>>> comments = map
>>> comments = map(lambda x: {u"body": re.sub("[a-z]", "m", x["body"])}, comments)
>>> comments = map(lambda x: {u"body": re.sub("[A-Z]", "M", x["body"])}, comments)
>>> comments = map(lambda x: {u"body": re.sub("[0-9]", "5", x["body"])}, comments)
>>> out = open("2013-06-27_HOUR-21_anon", "w")
>>> out.writelines(map(lambda x: json.dumps(x) + "\n", comments))
>>> out.close()
>>> exit()
$ ln -s 2013-06-27_HOUR-21_anon 2013-06-27_HOUR-21
$ git add 2013-06-27_HOUR-21_anon 2013-06-27_HOUR-21
```

Note that this loses some markdown structure, e.g. ordered bullets.

If you have original comment files you can point the symlink at them instead.
