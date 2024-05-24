# Vue3 keep-alive 下 onActivated 回调示例

在 Vue3 中，组件挂载后会触发 onMounted 回调

使用 keep-alive 展示的组件，如果组件名称在 include 列表内，当组件第一次挂载的时候并不是只会触发 onMounted 回调，而是会先后触发 onMounted 和 onActivated 两个回调

可以在 demo 页面中尝试，先将 About 页面加入到 keep-alive 的 cache 列表中，再点击跳转到 About 页面，在控制台会看到输出结果：

```shell
[About] onMounted
[About] onActivated
```

做这个记录的主要原因是之前一直对 onActivated 有误解，以为 onActivated 和 onMounted 是二选一回调的

最近在使用若依后台模版时还遇到了一个 bug：_在 keep-alive 页面直接刷新的时候不会触发 onActivated 回调，只会触发 onMounted 回调，如果是在其他页面新打开 keep-alive 页面，onActivated 又会正常回调_。困扰我几个小时之后，发现是因为若依是在 TagsView 的 onMounted 回调里面初始化 tags 列表，这时才将新页面的 Name 加入到 include 列表中......

后续将 onMounted 改为 onBeforeMount 就解决了