# Reading Party

## How to use
```
$ git clone 
$ cd contents/${BOOK_TITLE}/${EVENT_DATE}

# https://github.com/${YOUR_GITHUB_ACCOUNT}
$ touch ${YOUR_GITHUB_ACCOUNT}.md
$ tree contents
contents
└── Building-Event-Driven-Microservices  ## ${BOOK_TITLE}
    ├── 20210103                         ## ${EVENT_DATE}
    │   └── gkzz.md                      ## ${YOUR_GITHUB_ACCOUNT}
    └── info.md                          ## links of ${BOOK_TITLE}
```

## FAQ
- How to find my reading notes including "png"?
```
$ NAME=gkzz\
&& find contents/ -regex .*/*/${NAME}.md | xargs grep -n png
```