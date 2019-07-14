---
layout: default
title: Thử vài tính năng của markdown
---

# Headers: Bao nhiêu dấu # thì bấy nhiêu mức header
# H1
## H2
### H3
#### H4
##### H5
###### H6

# __Bôi đậm__, _nghiêng_
_Nghiêng_ (1 dấu sao hoặc 1 dấu gạch dưới)

__Đậm__ (2 dấu sao hoặc gạch dưới)

**Đậm _nghiêng và đậm_** (có thể kết hợp giữa chúng).

~~Gạch chéo~~

# Lists
1. Nếu bắt đầu bằng 1 chấm (1.) thì liệt kê có thứ tự, sau khi xuống dòng thì đánh số hay dấu *, -, + đều hiểu là thứ tự mới
- Bắt đầu bằng dấu - nhưng vẫn hiện ra thứ tự 2

  - Thụt vào ít nhất 2 dấu cách để bắt đầu liệt kê không thứ tự
  - Bắt đầu bằng - hay dấu + ở đầu đều liệt kê được
      - Thụt vào thêm 4 dấu cách nữa để liệt kê mức thấp hơn

  Enter xuống 1 dòng, thụt vào 1 hay nhiều dấu cách để căn lề một đoạn

  Thêm một đoạn nữa  
  Dòng trên đánh 2 dấu cách rồi enter là xuống dòng nhưng không ngắt đoạn (cách dòng ít hơn)

# Links  
Hai cách để chèn link

[I'm an inline-style link](https://www.google.com) --> [dấu ngoặc vuông là tên xuất hiện trên văn bản], (theo sau là dấu ngoặc đơn chứa link thực sự)

[I'm an inline-style link with title](https://www.google.com "Google's Homepage") --> sau link trong dấu ngoặc đơn là cặp nháy kép chứa title link, khi đặt chuột vào sẽ nổi title lên

[I'm a reference-style link][Arbitrary case-insensitive reference text] --> 2 cặp dấu ngoặc vuông, dấu ngoặc vuông thứ 2 chứa link có thể điền vào sau

[I'm a relative reference to a repository file](../blob/master/LICENSE)

[You can use numbers for reference-style link definitions][1]

Or leave it empty and use the [link text itself].

URLs and URLs trong dấu ngoặc nhọn được hiểu là link luôn. 
http://www.example.com or <http://www.example.com>.

Dưới chỗ này trong file markdown là một loạt các link để chèn vào đoạn trên

[arbitrary case-insensitive reference text]: https://www.mozilla.org
[1]: http://slashdot.org
[link text itself]: http://www.reddit.com

# Images
Chèn tương tự link, ngoại trừ trước dấu ngoặc vuông đầu có dấu chấm than ![]  
Đây là kết quả:  
Inline-style: 
![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 1")

Reference-style: 
![alt text][logo]

[logo]: https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 2"


# Code and Syntax Highlighting
Chèn đoạn code trong 3 dấu gạch ngược (chỗ dẫu ~) trên đầu như này ```python (enter) code ở đây (enter) ```

```javascript
var s = "JavaScript syntax highlighting";
alert(s);
```
 
```python
s = "Python syntax highlighting"
print s
```
 
```
No language indicated, so no syntax highlighting. 
But let's throw in a <b>tag</b>.
```

# Bảng
Tables aren't part of the core Markdown spec, but they are part of GFM and Markdown Here supports them. They are an easy way of adding tables to your email -- a task that would otherwise require copy-pasting from another application.

Colons can be used to align columns.

| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |

There must be at least 3 dashes separating each header cell.
The outer pipes (|) are optional, and you don't need to make the 
raw Markdown line up prettily. You can also use inline Markdown.

Markdown | Less | Pretty
--- | --- | ---
*Still* | `renders` | **nicely**
1 | 2 | 3
Colons can be used to align columns.

# Trích dẫn: Blockquotes
Dùng dấu lớn hơn  
> Blockquotes are very handy in email to emulate reply text.
> This line is part of the same quote.

### Trích dẫn đoạn dài Quote break.

> This is a very long line that will still be quoted properly when it wraps. Oh boy let's keep writing to make sure this is long enough to actually wrap for everyone. Oh, you can *put* **Markdown** into a blockquote. 
Blockquotes are very handy in email to emulate reply text. This line is part of the same quote.

# Inline HTML
You can also use raw HTML in your Markdown, and it'll mostly work pretty well.

<dl>
  <dt>Definition list</dt>
  <dd>Is something people use sometimes.</dd>

  <dt>Markdown in HTML</dt>
  <dd>Does *not* work **very** well. Use HTML <em>tags</em>.</dd>
</dl>

# Horizontal Rule
Three or more...

---

Hyphens

***

Asterisks

___

Underscores


#Line Breaks
My basic recommendation for learning how line breaks work is to experiment and discover -- hit <Enter> once (i.e., insert one newline), then hit it twice (i.e., insert two newlines), see what happens. You'll soon learn to get what you want. "Markdown Toggle" is your friend.

Here are some things to try out:

Here's a line for us to start with.

This line is separated from the one above by two newlines, so it will be a *separate paragraph*.

This line is also a separate paragraph, but...
This line is only separated by a single newline, so it's a separate line in the *same paragraph*.
Here's a line for us to start with.

This line is separated from the one above by two newlines, so it will be a separate paragraph.

This line is also begins a separate paragraph, but...
This line is only separated by a single newline, so it's a separate line in the same paragraph.

(Technical note: Markdown Here uses GFM line breaks, so there's no need to use MD's two-space line breaks.)

# YouTube Videos
They can't be added directly but you can add an image with a link to the video like this:

<a href="http://www.youtube.com/watch?feature=player_embedded&v=YOUTUBE_VIDEO_ID_HERE
" target="_blank"><img src="http://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg" 
alt="IMAGE ALT TEXT HERE" width="240" height="180" border="10" /></a>
Or, in pure Markdown, but losing the image sizing and border:

[![IMAGE ALT TEXT HERE](http://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg)](http://www.youtube.com/watch?v=YOUTUBE_VIDEO_ID_HERE)
Referencing a bug by #bugID in your git commit links it to the slip. For example #1.
# Công thức toán
Công thức toán ở đây gióng như LaTeX á, bắt đầu bằng dấu cặp dấu gạch \ và ( xong \ và ) nữa cho công thức trong dòng \(x^2+2x+1\), hoặc hai dấu đô la hoặc cặp \[ cho công thức tách dòng

$$\sum_{i=1}^{N}{x[n]e^{j\omega N}}$$
