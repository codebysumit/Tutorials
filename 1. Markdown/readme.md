# heading
---
__<u>Markdown Code:</u>__ 

```markdown
# heading 1
## heading 2
### heading 3
#### heading 4
##### heading 5
###### heading 6
```
__<u>Output:</u>__

# heading 1
## heading 2
### heading 3
#### heading 4
##### heading 5
###### heading 6
---

# Text Styling
---
__<u>Markdown Code:</u>__

```markdown
This is a **bold** word.

This is a alternative __bold__ word.

This is a *italic* word.

This is a alternative _italic_ word. 

~~Strike The line.~~
```

__<u>Output:<u/>__

This is a **bold** word.

This is a alternative __bold__ word.

This is a *italic* word.

This is a alternative _italic_ word. 

~~Strike The line.~~

---
# Use HTML in Markdown
---
__<u>Markdown Code:</u>__

```markdown
This text <u>color</u> is <b style="color: white; background: red;">RAD</b>.<br />
This is line **HTML** break.
```
c

This text <u>color</u> is <b style="color: white; background: red;">RAD</b>.<br />
This is line **HTML** break.

---

## Line break
---
**1. Soft line break:** add two spaces end of the line for geting soft line break.

__<u>Markdown Code:</u>__

```markdown
This is a frist line.  
This is a secound line.
```
__<u>Output:</u>__ 
This is a frist line.  
This is a secound line.

**2. Heard Line break:** add an Enter line break end of the line.

__<u>Markdown Code:</u>__

```markdown
This is hard line break.

This is hard line break.
```
__<u>Output:</u>__ 

This is hard line break.

This is hard line break.

---
## URL Link
---
__1. 1st Example:__
```markdown
[GOOGLE](https://www.googke.com)
```
__<u>Output:</u>__

[GOOGLE](https://www.googke.com)

__2. 2nd Example:__

__References link :__

```markdown
[YouTube][YTURL]

[YTURL]: https://youtube.com
```
__<u>Output:</u>__

[YouTube][YTURL]

[YTURL]: https://www.youtube.com
---

# Comments
---
__<u>Markdown Code:</u>__

```markdown
[comment]: <> (This is a comment)
[//]: <> (This is a comment)
```
__<u>Output:</u>__

[comment]: <> (This is a comment)
[//]: <> (This is a comment)
---
# Display Images
---
__<u>Markdown Code:</u>__

```markdown
![MyImg](img.jpg)

![MyImg][imgref]

[imgref]: img.jpg
```
__<u>Output:</u>__

![MyImg](img.jpg)

![MyImg][imgref]

[imgref]: img.jpg
---

# Quotes 
---
__<u>Markdown Code:</u>__

```markdown
> I am known that "I am not a good programmer.  
> I Love you.
>
> ***Text Style***
```
__<u>Output:</u>__

> I am known that "I am not a good programmer.  
> I Love you.
>
> ***Text Style***
---
# List
---
__<u>Markdown Code 1:</u>__

```markdown
- One
  - One
  - Two
- Two
- there
- Four
```

__<u>Output:</u>__

- One
  - One
  - Two
- Two
- there
- Four

__<u>Markdown Code 2:</u>__


```markdown
* One
    * One
    * Two
* Two
* there
* Four
```
__<u>Output:</u>__

* One
    * One
    * Two
* Two
* there
* Four

__<u>Markdown Code 3:</u>__


```markdown
1. One
    1. One
       1. Demo 1
          1. Demo 1
              1. So On.
          3. demo 2
       3. Demo 2
    3. Two
2. Two
```
__<u>Output:</u>__

1. One
    1. One
       1. Demo 1
          1. Demo 1
              1. So On.
          3. demo 2
       3. Demo 2
    3. Two
2. Two
---

# Code Snippets 
---
__<u>Markdown Code 1 (Python):</u>__
```markdown
    ```python
    print("Hello WWorld 👋!")
    ```
```
__<u>Output:</u>__

```python
print("Hello WWorld 👋!")
```
__<u>Markdown Code 2 (c++):</u>__

```markdown
    ```c++
    # include<iostream>
    using namespace std;
    
    int main(){
        cout << "Hello WWorld 👋!" << endl;
        return 0;
    }
    ```
```
__<u>Output:</u>__
```c++
# include<iostream>
using namespace std;

int main(){
    cout << "Hello WWorld 👋!" << endl;
    return 0;
}
```

__<u>Markdown Code 3:</u>__

```markdown
    ```
    !pip install numpy
    ```
```
__<u>Output:</u>__

```
!pip install numpy
```

__<u>Markdown Code 4 (sh):</u>__

```markdown
    ```sh
    mkdir "New Folder"
    ```
```
__<u>Output:</u>__

```sh
mkdir "New Folder"
```

# Table

__<u>Markdown Code:</u>__

```markdown
|Name|Age|Roll No.|Gender|
|----|---|--------|------|
|Sumit Das|19|24|M|
|Akash Kanji|19|2|M|
```

__<u>Output:</u>__

|Name|Age|Roll No.|Gender|
|----|---|--------|------|
|Sumit Das|19|24|M|
|Akash Kanji|19|2|M|

---

# Separate the lile

__<u>Markdown Code 1:</u>__

```markdown
---
```

__<u>Output:</u>__

---

__<u>Markdown Code 2:</u>__

```markdown
___
```

__<u>Output:</u>__

___
---

# Check Box Lists

__<u>Markdown Code:</u>__

```markdown
- [ ] Check Box is unchecked 
- [x] Check Box is checked
```
__<u>Output:</u>__

- [ ] Check Box is unchecked 
- [x] Check Box is checked
---
# Math & LateX

__<u>Markdown Code:</u>__

```markdown
X <sub>1</sub> and X <sub>2</sub>

X <sup>2</sup> = X * X

LateX in MD Inline: $\Phi^{2} + X =3$

LateX in MD Display: $$\Phi^{2} + X =3$$
```
__<u>Output:</u>__

X <sub>1</sub> and X <sub>2</sub>

X <sup>2</sup> = X * X

LateX in MD Inline: $\Phi^{2} + X =3$

LateX in MD Display: $$\Phi^{2} + X =3$$

