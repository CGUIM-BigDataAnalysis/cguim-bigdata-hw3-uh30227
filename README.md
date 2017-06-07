長庚大學 大數據分析方法 作業三
================



網站資料爬取
------------

``` r
##install.packages("rvest") ##安裝
library(rvest) ##載入
dataframeAll=NULL
for(i in 5289:5299){
url=paste0("http://www.ptt.cc/bbs/movie/index",i,".html",sep='')
PTT_Title = read_html(url) %>% html_nodes(".title") %>% html_text()
PTT_PushNum = read_html(url) %>% html_nodes(".nrec") %>% html_text()
PTT_Author = read_html(url) %>% html_nodes(".author") %>% html_text()
dataframe = data.frame(title = PTT_Title, PushNum=PTT_PushNum, Author=PTT_Author)
dataframeAll<-rbind(dataframeAll,dataframe)
}
```

爬蟲結果呈現
------------

``` r
knitr::kable(
    dataframeAll[1:120,c("title","PushNum","Author")])
```



解釋爬蟲結果
------------

``` r
##install.packages("jsonlite")
library(jsonlite)
myjson <- toJSON(dataframeAll)
str(dataframeAll)
table(dataframeAll$ Author)
```

(1)總共爬出220 篇文章，裡面共有3個變數:title、PushNum、Author
(2)沒有名字的作者最多，共有15篇沒屬名的文章，有屬名的文章以DantesChen的文章最多，共4篇

``` r
#這是R Code Chunk
```


這個版的內容很無聊
