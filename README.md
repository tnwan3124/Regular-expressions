# Regular expressions

# Introduction

### **What are regular expressions?**

Biểu thức chính quy (hay Regex) là các mẫu văn bản mà bạn định nghĩa để tìm kiếm tài liệu và khớp chính xác những gì bạn đang tìm kiếm.

### Tại sao tôi nên học cách sử dụng chúng? (**Why should I learn how to use them?)**

Ngay cả khi bạn sẽ không cần chúng sớm hay muộn, đó là một công cụ tuyệt vời để biết cách sử dụng. Nó sẽ giúp bạn có nhiều khả năng hơn trong CTF và có khả năng trở thành một nhà phát triển giỏi hơn nếu đó là mục tiêu của bạn. Bạn dành một ít thời gian để học nó và tiết kiệm cho mình rất nhiều thời gian về lâu dài bằng cách sử dụng nó.

### Tôi biết tất cả những điều đó, nhưng tôi lười biếng. (**I know all that, but I'm lazy.)**

Đây là một hướng dẫn dành cho người lười biếng. Có một chút đọc, và sau đó bạn học bằng cách làm.

### Nút 'Triển khai' ở đâu? (**Where's the 'Deploy' button?)**

Không có máy nào để triển khai. Có hai cách để kiểm tra các biểu thức của bạn. Hoặc là:

- tạo một tệp văn bản với một số đoạn văn bản thử nghiệm (trong máy Unix) và sau đó sử dụng egrep <pattern> <file> để xem những gì khớp và những gì không khớp, hoặc
- sử dụng trình soạn thảo trực tuyến như [https://regexr.com/](https://regexr.com/). Bạn có thể thêm văn bản của riêng mình vào trường "Văn bản", sau đó nhập biểu thức (mẫu) của bạn vào trường "Biểu thức".

Tôi khuyên bạn nên làm theo cách thứ hai.

---

# Charsets

Khi tìm kiếm một chuỗi cụ thể trong một tệp hoặc khối văn bản, bạn có thể tìm kiếm trực tiếp bằng cách sử dụng `grep 'string' <file>`. Tuy nhiên, nếu bạn muốn tìm kiếm các **mẫu** văn bản thì sao? Ví dụ: bạn có thể muốn tìm một từ bắt đầu bằng một chữ cái cụ thể hoặc bất kỳ từ nào kết thúc bằng số. Đó chính là lúc **Biểu thức chính quy (Regular Expressions)** trở nên hữu ích.
Cả hai vấn đề đã đề cập trước đó đều có thể được giải quyết bằng cách sử dụng **bộ ký tự (charsets)**. Một bộ ký tự được định nghĩa bằng cách đặt các ký tự hoặc phạm vi ký tự mà bạn muốn khớp vào trong **dấu ngoặc vuông [ ]**. Sau đó, nó tìm thấy **mọi lần xuất hiện** của **mẫu** bạn đã định nghĩa trong tệp/văn bản bạn đang tìm kiếm.

`[abc]` sẽ khớp với `a, b, và c` (mọi lần xuất hiện của mỗi ký tự)
`[abc]zz` sẽ khớp với `azz, bzz và czz.`
Bạn cũng có thể dùng `-` dấu gạch ngang để định nghĩa phạm vi:
`[a-c]zz` thì tương tự như trên.
Và bạn có thể kết hợp các phạm vi:
`[a-cx-z]zz` sẽ khớp với `azz, bzz, czz, xzz, yzz, và zzz.`
Đặc biệt, điều này có thể được sử dụng để khớp với bất kỳ ký tự chữ cái nào:
`[a-zA-Z]` sẽ khớp với mọi ký tự riêng lẻ (viết thường hoặc viết hoa).
Bạn có thể sử dụng các con số cũng vậy:
`file[1-3]` sẽ khớp với `file1, file2, và file3.`
Sau đó, đây là 1 cách để **loại trừ** các ký tự từ một bộ ký tự với ký hiệu mũ "**`^`**", và bao gồm mọi thứ khác.
`[^k]ing` sẽ khớp với `ring, sing, $ing`, nhưng không khớp với `king`.
Tất nhiên, bạn cũng có thể loại trừ các bộ ký tự, không chỉ là những ký tự đơn lẻ.
`[^a-c]at` sẽ khớp với `fat và hat`, nhưng không khớp với `bat hoặc cat`.

**Lưu ý 1:** Đừng nhầm lẫn giữa chuỗi và bộ ký tự. Bộ ký tự `[abc]` sẽ khớp với chuỗi `abc`, nhưng cũng khớp với `cba` và `ca`. Nó không khớp với toàn bộ chuỗi, mà là **mỗi lần xuất hiện** của các ký tự được chỉ định trong chuỗi đó.
**Lưu ý 2:** Khi chỉ định các bộ ký tự, bạn nên gõ các chữ cái theo cùng thứ tự chúng xuất hiện trong câu hỏi, để tránh gõ một thứ gì đó đúng nhưng không phải là câu trả lời chính xác.
**Lưu ý 3:** Trả lời một số câu hỏi này sẽ khá phức tạp. Thông thường, có nhiều mẫu khác nhau có thể khớp với các chuỗi cụ thể. Điều đó có nghĩa là (như đã nêu trong lưu ý trước) bạn có thể tìm thấy một giải pháp phù hợp nhưng không phải là câu trả lời đúng cho phòng này (vì chỉ có thể có một câu trả lời đúng). Câu trả lời đúng thường là biểu thức chính quy hiệu quả nhất cho câu hỏi đó.

### Hiệu quả trong ngữ cảnh này có 2 nghĩa:

1. **Hãy cụ thể.** Ví dụ: bạn *có thể* khớp bất kỳ ký tự nào từ a đến z bằng cách sử dụng bộ ký tự       `[a-z]`. Nhưng nếu câu hỏi chỉ yêu cầu bạn khớp các ký tự từ a đến c, bạn *nên* sử dụng bộ ký tự `[a-c]`, không phải `[a-z]`.
2. Đừng quá cụ thể. Trái ngược với ví dụ trước, nếu một câu hỏi yêu cầu bạn khớp với các ký tự a, c, f, r, s, z, thì biểu thức khớp với những ký tự cụ thể đó sẽ trở nên dài hơn và phức tạp hơn. Vì vậy, sẽ hợp lý hơn nếu sử dụng `[a-z]`, bởi vì nó ngắn gọn và đơn giản.

**Nhắc lại,** không thể có một giải pháp đúng duy nhất. Vì vậy, nếu bạn đã thử nghiệm giải pháp của mình và nó hoạt động, bạn có thể nghỉ ngơi một chút và quay lại sau, hoặc hỏi gợi ý trên Discord, nhưng đừng nản lòng.

---

# Wildcards and optional characters

Ký tự đại diện (wildcard) được sử dụng để khớp với bất kỳ ký tự đơn lẻ nào (ngoại trừ dấu xuống dòng) là dấu chấm `.`. Điều đó có nghĩa là `a.c` sẽ khớp với `aac`, `abc`, `a0c`, `a!c`, v.v.

Ngoài ra, bạn có thể đặt một ký tự là tùy chọn trong mẫu của mình bằng cách sử dụng dấu chấm hỏi `?`. Điều đó có nghĩa là `abc?` sẽ khớp với cả `ab` và `abc`, vì `c` là tùy chọn.

**Lưu ý:** Nếu bạn muốn tìm kiếm một dấu chấm `.` theo nghĩa đen (tức là tìm kiếm chính ký tự dấu chấm chứ không phải bất kỳ ký tự nào), bạn phải **escape** nó bằng một dấu gạch chéo ngược `\`. Điều đó có nghĩa là `a.c` sẽ khớp với `a.c`, nhưng cũng khớp với `abc`, `a@c`, v.v. Nhưng `a\.c` sẽ chỉ khớp với `a.c`.

---

# Metacharacters and repetitions

Có những cách dễ dàng hơn để khớp với các bộ ký tự lớn hơn. Ví dụ: `\d` được sử dụng để khớp với bất kỳ một chữ số nào. Dưới đây là bảng tham khảo:

- `\d` khớp với một chữ số, như `9`
- `\D` khớp với một ký tự không phải chữ số, như `A` hoặc `@`
- `\w` khớp với một ký tự chữ hoặc số, như `a` hoặc `3`
- `\W` khớp với một ký tự không phải chữ hoặc số, như `!` hoặc `#`
- `\s` khớp với một ký tự khoảng trắng (dấu cách, tab và xuống dòng)
- `\S` khớp với mọi thứ khác (ký tự chữ và số và ký hiệu)

**Lưu ý:** Dấu gạch dưới `_` được bao gồm trong metacharacter `\w` chứ không phải trong `\W`. Điều đó có nghĩa là `\w` sẽ khớp với mọi ký tự đơn lẻ trong `test_file`.

Thông thường, chúng ta muốn một mẫu khớp với nhiều ký tự cùng loại liên tiếp, và chúng ta có thể làm điều đó với các phép lặp. Ví dụ: `{2}` được sử dụng để khớp với ký tự đứng trước nó (hoặc metacharacter, hoặc bộ ký tự) hai lần liên tiếp. Điều đó có nghĩa là `z{2}` sẽ khớp chính xác với `zz`.

Dưới đây là bảng tham khảo cho mỗi phép lặp cùng với số lần nó khớp với mẫu đứng trước:

- `{12}` - chính xác 12 lần.
- `{1,5}` - từ 1 đến 5 lần.
- `{2,}` - 2 lần trở lên.
- `*` - 0 lần trở lên.
- `+` - 1 lần trở lên.

---

# Starts with/ ends with, groups, and either/ or

Đôi khi, việc chỉ định rằng chúng ta muốn tìm kiếm theo một mẫu nhất định ở đầu hoặc cuối một dòng là rất hữu ích. Chúng ta làm điều đó với các ký tự sau:

- `^` - bắt đầu với
- `$` - kết thúc với

Ví dụ: nếu bạn muốn tìm kiếm một dòng **bắt đầu bằng** `abc`, bạn có thể sử dụng `^abc`.

Nếu bạn muốn tìm kiếm một dòng **kết thúc bằng** `xyz`, bạn có thể sử dụng `xyz$`.

**Lưu ý:** Ký hiệu mũ `^` được sử dụng để loại trừ một bộ ký tự khi được **đặt trong dấu ngoặc vuông**, nhưng khi không có dấu ngoặc vuông, nó được sử dụng để chỉ định phần đầu của một từ.

Bạn cũng có thể định nghĩa các nhóm bằng cách đặt một mẫu trong **dấu ngoặc đơn**. Chức năng này có thể được sử dụng theo nhiều cách khác nhau nằm ngoài phạm vi của hướng dẫn này. Chúng ta sẽ sử dụng nó để định nghĩa một mẫu **"hoặc cái này / hoặc cái kia"**, và cũng để lặp lại các mẫu. Để diễn tả "hoặc" trong Regex, chúng ta sử dụng dấu gạch đứng `|`.

Ví dụ về mẫu "hoặc cái này / hoặc cái kia": mẫu `during the (day|night)` sẽ khớp với cả hai câu sau: `during the day` và `during the night`.

Ví dụ về lặp lại mẫu: mẫu `(no){5}` sẽ khớp với câu `nonononono`.

---

# Practical

## Charsets (Vấn đề đọc hiểu không cần giải thích)

### Câu hỏi

1. Match all of the following characters: **c, o, g**

**Correct Answer: [cog]**

1. Match all of the following words: **cat, fat, hat**

**Correct Answer: [cfh]at**

1. Match all of the following words: **Cat, cat, Hat, hat**

**Correct Answer: [cChH]at**

1. Match all of the following filenames: **File1, File2, file3, file4, file5, File7, file9**

**Correct Answer: [fF]ile[1-9]**

1. Match all of the filenames of question 4, **except** "File7" (use the hat symbol)

**Correct Answer: [fF]ile[^7]**

---

## Wildcards and optional characters

### Câu hỏi (Vấn đề đọc Hiểu)

1. Match all of the following words: **Cat, fat, hat, rat**

**Correct Answer: .at**

1. Match all of the following words: **Cat, cats**

**Correct Answer: [Cc]ats?**

1. Match the following domain name: **cat.xyz**

**Correct Answer: cat\.xyz**

1. Match all of the following domain names: **cat.xyz, cats.xyz, hats.xyz**

**Correct Answer: [ch]ats?\.xyz**

1. Match every 4-letter string that **doesn't end** in any letter from **n to z**

**Correct Answer: …[^n-z]**

1. Match **bat, bats, hat, hats, but not rat or rats** (use the hat symbol)

**Correct Answer:[bh]ats?[^r] (1) Hoặc [^r]ats? (2) {Trường hợp 1 đúng với yêu cầu đề bài. Nhưng muốn khớp với các chuỗi trừ mỗi r thì dùng trường hợp 2}**

---

## Metacharacters and repetitions

### Câu hỏi

1. Match the following word: **catssss**

**Correct Answer: cats{4}**

1. Match all of the following words (use the ***** sign): **Cat, cats, catsss**

**Correct Answer: [cC]ats***

1. Match all of the following sentences (use the + sign): **regex go br, regex go brrrrrr**

**Correct Answer: regex go br+**

1. Match all of the following filenames: **ab0001, bb0000, abc1000, cba0110, c0000** (don't use a metacharacter)

**Correct Answer: [abc]{1,3}[01]{4}**

**[abc]{1,3}** nó chỉ định bộ ký tự đứng trước xuất hiện ít nhất 1 lần và nhiều nhất là 3 lần.

**[01]**: Một bộ ký tự khác, khớp với '0' hoặc '1'.

**{4}**: Một định lượng khác, chỉ định rằng bộ ký tự đứng trước nó (`[01]`) phải xuất hiện chính xác 4 lần.

1. Match all of the following filenames: **File01, File2, file12, File20, File99**

**Correct Answer: [fF]ile\d{1,2}**

1. Match all of the following folder names: **kali tools, kali     tools**

**Correct Answer: kali`\s+`tools**

1. Match all of the following filenames: **notes~, stuff@, gtfob#, lmaoo!**

**Correct Answer: \w\w\w\w\w\W hoặc \w{5}\W**

1. Match the string in quotes (use the * sign and the \s, \S metacharacters): "**2f0h@f0j0%!     a)K!F49h!FFOK**"

**Correct Answer: \S*\s*\S***

1. Match **every 9-character string** (with letters, numbers, and symbols) that **doesn't end in a "!" sign**

**Correct Answer:  \S{8}[^!]**

1. Match all of these filenames (use the + symbol): **.bash_rc, .unnecessarily_long_filename, and note1**

**Correct Answer: \.?\w+** 

---

## Starts with/ ends with, groups, and either/ or

### Câu hỏi

1. Match every string that **starts with "Password:"** followed by any 10 characters **excluding "0"**

**Correct Answer: ^Password: [^0]{10}**

1. Match "**username:** " in the beginning of a line (**note the space!**)

**Correct Answer:^username:\s**

1. Match every line that **doesn't start with a digit** (use a metacharacter)

**Correct Answer: ^\D**

1. Match this string **at the end of a line: EOF$**

**Correct Answer: EOF\$$**

1. Match all of the following sentences:
- **I use nano**
- **I use vim**

**Correct Answer: i use (nano|vim)**

1. Match all lines that **start with $**, f**ollowed by any single digit, followed by $, followed by one or more non-whitespace characters**

**Correct Answer: \$\d\$\S+**

1. Match every **possible IPv4 IP address** (use metacharacters and groups)

**Correct Answer: (\d{1,3}\.){3}\d{1,3}**

- `(\d{1,3}\.)`: Nhóm này khớp với một chuỗi từ 1 đến 3 chữ số, theo sau bởi một dấu chấm. Ví dụ: "123.", "1.", "255."
- `(\d{1,3}\.){3}`: Nhóm trên được lặp lại 3 lần. Điều này khớp với 3 nhóm số và dấu chấm liên tiếp, ví dụ: "192.168.0." hoặc "10.0.0."
- `\d{1,3}`: Cuối cùng, biểu thức khớp với một chuỗi từ 1 đến 3 chữ số. Đây là phần cuối cùng của địa chỉ IP.
1. Match all of **these emails while also adding the username and the domain name** (not the TLD) in separate groups (use \w): [hello@tryhackme.com](mailto:hello@tryhackme.com), [username@domain.com](mailto:username@domain.com), [dummy_email@xyz.com](mailto:dummy_email@xyz.com)

**Correct Answer: (\w+)@(\w+)\.com**