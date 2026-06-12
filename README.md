# Mẫu Báo Cáo LaTeX Đồ Án / Luận Văn

Đây là mẫu báo cáo được thiết kế sẵn cho sinh viên, đặc biệt là các dự án/đồ án (VD: Hệ điều hành và Mạng máy tính). Mẫu đã được cấu hình tự động đánh mục lục, Việt hoá toàn bộ các tiêu đề, và căn chỉnh lề chuẩn để in một mặt.

## 1. Cấu trúc thư mục

- `main.tex`: File gốc chứa cấu trúc tổng thể của toàn bộ báo cáo.
- `packages.tex`: Nơi khai báo tất cả các gói thư viện (packages) cần dùng.
- `titlepage.tex`: Chứa mã định dạng cho trang bìa.
- `abstract.tex`: Chứa phần Tóm tắt của báo cáo.
- `chapters/`: Thư mục chứa các chương của báo cáo (Mở đầu, Tổng quan, Phương pháp, v.v.).
- `images/`: Thư mục lưu trữ toàn bộ hình ảnh.
- `tables/`: Thư mục lưu trữ toàn bộ bảng.
- `references.bib`: File lưu trữ thông tin các tài liệu tham khảo (theo chuẩn BibTeX).

## 2. Hướng dẫn cài đặt để gõ Offline

Để biên dịch (compile) LaTeX trên máy tính cá nhân mà không cần dùng Overleaf, bạn cần cài đặt 2 thành phần chính: một **Trình biên dịch (Compiler)** và một **Trình soạn thảo (Editor)**.

### Bước 2.1. Cài đặt Trình biên dịch (Compiler)
Đây là "bộ máy" giúp dịch code LaTeX thành file PDF. Bạn chọn 1 trong các phần mềm sau (Khuyên dùng **TeX Live** hoặc **MiKTeX**):

- **Windows:** 
  - [TeX Live](https://tug.org/texlive/acquire-netinstall.html) (Bản đầy đủ, khuyên dùng, dung lượng lớn).
  - [MiKTeX](https://miktex.org/download) (Bản nhẹ hơn, tự động tải gói khi cần).
- **macOS:** 
  - [MacTeX](https://tug.org/mactex/) (Phiên bản TeX Live dành cho Mac).
- **Linux:** Cài đặt thông qua Terminal (VD: `sudo apt-get install texlive-full` trên Ubuntu).

### Bước 2.2. Cài đặt Trình soạn thảo (Editor)
Đây là phần mềm để bạn gõ code. Bạn có thể chọn 1 trong các phần mềm sau:

- **[Visual Studio Code (VS Code)](https://code.visualstudio.com/)**: Rất phổ biến. Sau khi tải về, bạn vào mục Extensions và cài thêm tiện ích **LaTeX Workshop**.
- **[TeXstudio](https://www.texstudio.org/)**: Phần mềm chuyên dụng chỉ dành riêng cho LaTeX, có sẵn nút bấm biên dịch và xem PDF tiện lợi.

### Bước 2.3. Cài đặt Strawberry Perl (Dành riêng cho Windows)
Lệnh `makeglossaries` (dùng để tạo danh mục từ viết tắt) được viết bằng ngôn ngữ Perl. Vì vậy, trên Windows, bạn bắt buộc phải cài đặt Perl để máy tính có thể chạy được lệnh này.

1. Truy cập trang web: [Strawberry Perl](https://strawberryperl.com/)
2. Tải về phiên bản mới nhất và tiến hành cài đặt.
3. **Thêm vào biến môi trường (PATH):** Thông thường, bộ cài đặt Strawberry Perl sẽ tự động thêm đường dẫn vào PATH. Nếu lệnh `makeglossaries` vẫn báo lỗi, bạn làm thủ công như sau:
   - Mở Start Menu, tìm kiếm **"Environment Variables"** $\rightarrow$ Chọn *Edit the system environment variables*.
   - Nhấn nút **Environment Variables...**
   - Ở phần *System variables* (hoặc *User variables*), tìm biến **Path**, chọn nó và nhấn **Edit...**
   - Nhấn **New** và thêm đường dẫn tới thư mục `perl\bin` và `c\bin` của Strawberry Perl (thường là `C:\Strawberry\perl\bin` và `C:\Strawberry\c\bin`).
   - Nhấn OK để lưu lại và **khởi động lại máy tính (hoặc VS Code / Terminal)** để nhận PATH mới.

## 3. Cách biên dịch (Compile) dự án này

Vì dự án có sử dụng tài liệu tham khảo (biblatex) và danh mục từ viết tắt (glossaries), thứ tự biên dịch chuẩn để mọi thứ hiển thị đúng là:

1. **pdflatex** `main.tex` (để tạo cấu trúc cơ bản)
2. **biber** `main` (để lấy danh sách tài liệu tham khảo)
3. **makeglossaries** `main` (để tạo danh mục từ viết tắt)
4. **pdflatex** `main.tex` (để nhúng tài liệu và từ viết tắt vào PDF)
5. **pdflatex** `main.tex` (chạy lần cuối để đảm bảo các đánh số trang, liên kết được căn chuẩn)

*(Nếu dùng VS Code với LaTeX Workshop, bạn có thể thiết lập Recipe `latexmk` hoặc `pdflatex ➞ biber ➞ pdflatex` để phần mềm tự động làm các bước này).*

## 4. Hướng dẫn gõ LaTeX cơ bản

### Thêm Chương, Mục
Bạn nên tạo file `.tex` mới trong thư mục `chapters/`, sau đó dùng lệnh `\input{chapters/ten_file}` vào `main.tex`.
```latex
\chapter{Tên chương mới}
\section{Mục lớn}
\subsection{Mục nhỏ}
\subsubsection{Mục nhỏ hơn}
```

### Chèn Hình Ảnh
Hình ảnh nên được lưu trong thư mục `images/`.
```latex
\begin{figure}[H] % [H] để cố định vị trí hình
    \centering
    \includegraphics[width=0.8\textwidth]{ten_hinh_anh.png} % Không cần ghi thư mục images/
    \caption{Ghi chú cho hình ảnh}
    \label{fig:ten_hinh}
\end{figure}
```
Tham chiếu tới hình ảnh trong văn bản: `Như ta thấy ở Hình \ref{fig:ten_hinh}...`

### Chèn Bảng
```latex
\begin{table}[H]
    \centering
    \caption{Tiêu đề của bảng}
    \vspace{0.2cm}
    \begin{tabular}{|c|c|l|}
        \hline
        \textbf{STT} & \textbf{Cột 2} & \textbf{Cột 3} \\
        \hline
        1 & Dữ liệu 1 & Dữ liệu 2 \\
        \hline
    \end{tabular}
    \label{tab:ten_bang}
\end{table}
```

### Trích dẫn Tài liệu tham khảo (Theo thứ tự xuất hiện [1], [2])
1. Thêm tài liệu vào file `references.bib`:
```bibtex
@article{einstein,
    author = "Albert Einstein",
    title = "{Zur Elektrodynamik bewegter K{\"o}rper}. ({German})",
    journal = "Annalen der Physik",
    year = "1905"
}
```
2. Gọi tài liệu trong văn bản:
```latex
Theo nghiên cứu của tác giả \cite{einstein}...
```
*Văn bản sẽ tự động đánh số dạng [1], [2] theo thứ tự gọi hàm cite từ trên xuống dưới.*

### Sử dụng Từ viết tắt
1. Định nghĩa từ viết tắt (có thể đặt ở file `packages.tex` hoặc đầu `main.tex`):
```latex
\newacronym{os}{OS}{Operating System - Hệ điều hành}
```
2. Gọi từ viết tắt trong văn bản:
```latex
Windows là một \gls{os} phổ biến.
```
Lần gọi đầu tiên, nó sẽ in ra: *Operating System - Hệ điều hành (OS)*. Các lần gọi sau sẽ chỉ in ra: *OS*. Danh sách này sẽ tự động xuất hiện ở phần "Danh mục các từ viết tắt".

## 5. Các cấu hình đặc biệt đã được thiết lập sẵn
- **Lề trang:** Khổ A4, Trái 3cm, Phải 2cm, Trên 2cm, Dưới 2.5cm (Chuẩn in báo cáo một mặt).
- **Số trang:** Đặt ở góc dưới cùng bên phải.
- **Ngôn ngữ:** Hỗ trợ gõ tiếng Việt có dấu (`\usepackage[utf8]{inputenc}`). Đã Việt hoá tự động các cụm từ "Chapter" thành "Chương", "Table of Contents" thành "Mục lục", "References" thành "Tài liệu tham khảo", v.v.
- **Thứ tự trang đầu:** Tóm tắt $\rightarrow$ Danh mục Hình ảnh $\rightarrow$ Danh mục Bảng $\rightarrow$ Danh mục Từ viết tắt $\rightarrow$ Mục lục.
