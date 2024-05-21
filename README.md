# Encryption-Decryption App

This is a simple graphical user interface (GUI) application built using Python's Tkinter library. The app allows users to encrypt and decrypt text messages using Base64 encoding and decoding. The encryption and decryption processes are password-protected.

## Features

- **Encrypt Text:** Convert plain text to Base64 encoded text.
- **Decrypt Text:** Convert Base64 encoded text back to plain text.
- **Password Protection:** Requires a password to perform encryption and decryption operations.
- **Reset Functionality:** Clear the text and password input fields.

## Prerequisites

- Python 3.x
- Tkinter library (usually comes pre-installed with Python)
- Base64 library (standard library in Python)

## Installation

1. Ensure you have Python installed. You can download it from [python.org](https://www.python.org/).

2. Clone this repository or download the source code.

3. Ensure you have the `keys.png` image file in the same directory as the script. This image will be used as the icon for the application window.

## Usage

1. Run the `main.py` script:
    ```sh
    python main.py
    ```

2. The application window will appear with fields to enter text and a secret key.

3. Enter the text you want to encrypt or decrypt in the first text box.

4. Enter the password (`1234`) in the "secret key" field.

5. Click on the "ENCRYPT" button to encode the text or "DECRYPT" button to decode it.

6. The result will be displayed in a new window.

## Code Explanation

The application consists of the following main components:

- **main_screen():** Initializes the main window, sets up the layout, and defines the reset functionality.
- **encrypt():** Encrypts the input text using Base64 encoding and displays the result in a new window.
- **decrypt():** Decrypts the Base64 encoded text and displays the result in a new window.

### main_screen()

```python
def main_screen():
    global screen
    global code
    global text1

    screen = Tk()
    screen.geometry("375x398")

    image_icon = PhotoImage(file="keys.png")
    screen.iconphoto(False, image_icon)

    screen.title("Encryption-decryption App")

    def reset():
        code.set("")
        text1.delete(1.0, END)

    Label(text="Enter text for encryption and decryption", fg="black", font=("calibri", 13)).place(x=10, y=10)
    text1 = Text(font="Roboto 20", bg="white", relief=GROOVE, wrap=WORD, bd=0)
    text1.place(x=10, y=50, width=355, height=100)

    Label(text="Enter secret key for encryption and decryption", fg="black", font=("calibri", 13)).place(x=10, y=170)

    code = StringVar()
    Entry(textvariable=code, width=19, bd=0, font=("arial", 25), show="*").place(x=10, y=200)

    Button(text="ENCRYPT", height="2", width=23, bg="#ed3833", fg="white", bd=0, command=encrypt).place(x=10, y=250)
    Button(text="DECRYPT", height="2", width=23, bg="#00bd56", fg="white", bd=0, command=decrypt).place(x=200, y=250)
    Button(text="RESET", height="2", width=50, bg="#1089ff", fg="white", bd=0, command=reset).place(x=10, y=300)

    screen.mainloop()
```

### encrypt()

```python
def encrypt():
    password = code.get()

    if password == "1234":
        screen1 = Toplevel(screen)
        screen1.title("encryption")
        screen1.geometry("400x200")
        screen1.configure(bg="#ed3833")

        message = text1.get(1.0, END)
        encode_message = message.encode("ascii")
        base64_bytes = base64.b64encode(encode_message)
        encrypt = base64_bytes.decode("ascii")

        Label(screen1, text="ENCRYPT", font="arial", fg="white", bg="#ed3833").place(x=10, y=0)
        text2 = Text(screen1, font="Roboto 10", bg="white", relief=GROOVE, wrap=WORD, bd=0)
        text2.place(x=10, y=40, width=380, height=150)

        text2.insert(END, encrypt)

    elif password == "":
        messagebox.showerror("encryption", "Input Password")

    elif password != "1234":
        messagebox.showerror("encryption", "Invalid Password")
```

### decrypt()

```python
def decrypt():
    password = code.get()

    if password == "1234":
        screen2 = Toplevel(screen)
        screen2.title("decryption")
        screen2.geometry("400x200")
        screen2.configure(bg="#00bd56")

        message = text1.get(1.0, END)
        decode_message = message.encode("ascii")
        base64_bytes = base64.b64decode(decode_message)
        decrypt = base64_bytes.decode("ascii")

        Label(screen2, text="DECRYPT", font="arial", fg="white", bg="#00bd56").place(x=10, y=0)
        text2 = Text(screen2, font="Roboto 10", bg="white", relief=GROOVE, wrap=WORD, bd=0)
        text2.place(x=10, y=40, width=380, height=150)

        text2.insert(END, decrypt)

    elif password == "":
        messagebox.showerror("encryption", "Input Password")

    elif password != "1234":
        messagebox.showerror("encryption", "Invalid Password")
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
