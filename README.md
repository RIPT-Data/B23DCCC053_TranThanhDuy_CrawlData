# Introduction to Crawl Data
## Mục lục
- [Giới thiệu](#giới-thiệu)
- [Định nghĩa Crawl Data](#định-nghĩa-crawl-data)
- [Ứng dụng để Crawl Data](#ứng-dụng-crawl-data)
- [Demo chạy Data]()
    - [Setup trước khi làm Crawl Data](#setup-trước-khi-làm-crawl-data)
    - [Các bước thực hiện Crawl Data bằng Python](#các-bước-thực-hiện-crawl-data)
    - [Chương trình Python](#chương-trình-python)
- [Kết luận]()
- [Tài liệu tham khảo]()
## Giới thiệu
Đối với các Data Analyst, Data Engineer cũng như Data Scientist, việc cào dữ liệu (Crawl Data), một từ ngữ chuyên ngành có lẽ không quá xa lạ đối với họ, là một trong những bước quan trọng nhất trong việc xử lý dữ liệu của những người làm về lĩnh vực ấy. Vậy Crawl Data là gì? Tại sao nó lại quan trọng đến thế? Báo cáo này sẽ giúp cho mọi người có một cái nhìn rõ ràng, chi tiết hơn về những thông tin hữu ích của Crawl Data dưới đây.
## Định nghĩa Crawl Data
Crawl Data là quá trình thu thập dữ liệu của công cụ tìm kiếm nhằm tìm nội dung mới hoặc cập nhật những thay đổi trên trang cũ. Những định dạng được thu thập dữ liệu gồm: HTML, Hình ảnh, Video,... 

Dữ liệu thu về trong từng lần Crawl Data sẽ gửi tới máy chủ tìm kiếm kèm theo thời gian hoàn tất Crawl trước đó để tổng hợp, phân tích trước khi đưa ra quyết định Index
> Index là quá trình xếp hạng thứ bậc tìm kiếm của website theo từng nội dung tìm kiếm.
## Ứng dụng Crawl Data
- Phân tích thị trường:
    - Theo dõi giá cá: Có thể cào dữ liệu để thu thập thông tin về giá cả sản phẩm từ các trang thương mai điện tử và từ đó điều chỉnh chính lược giá.
    - Nhu cầu và xu hướng: Cào dữ liệu từ các đánh giá trên mạng xã hội dể có thể phân tích các xu hướng sản phẩm và nhu cầu của người tiêu dùng.
- Nghiên cứu và phân tích:
    - Phân tích đối thủ: Có thể cào dữ liệu để thu thập thông tin về đối thủ cạnh tranh => Hiểu được rõ chiến lược của họ
    - Thu thập dữ liệu cho nghiên cứu: Cào dữ liệu để phục vụ cho các bài báo, nghiên cứu khoa học

Ngoài ra còn nhiều ứng dụng khác như phân tích cảm xúc, tổng hợp tin tức,...
## Demo chạy Crawl Data
### Setup trước khi làm Crawl Data:
- Công cụ: Hiện nay có rất nhiều công cụ có thể sử dụng, phổ biến là:
    + BotGoogle
    + Thư viện BeautifulSoup4 hoặc Scrapy của Python
    + Thư viện Selenium của Java
    + Ngoài ra còn nhiều công cụ khác...
    
    Tuy vậy, công cụ được sử dụng trong bài báo cáo này để cào dữ liệu trong Demo này sẽ là BeautifulSoup4 của Python.
- Cách cài đặt:
- Trang web để Crawl Data: https://www.formula1.com/en/results/2024/drivers
    
    Sử dụng BXH các tay đua trong F1 cũng như kết hợp việc cào dữ liệu để có thể xuất ra được danh sách BXH các tay đua.
### Các bước thực hiện Crawl Data
- Tải Python xuống từ trang web và cài đặt: https://www.python.org/downloads/ 
- Tạo folder mới, đặt tên tùy ý. (Ở đây đặt tên là CrawlerData)
- Click chuột phải vào CrawlerData, sau đó ta chọn Open in CMD hoặc Open in Git Bash (Nếu như đã cài Git Bash)
- Lập tức gõ lệnh này để tự động mở các trình duyệt code
```
code .
```
- Tạo môi trường ảo của Python:
```
python3 -m venv environment-name
```
- Activate môi trường ảo:
```
venv/bin/activate.bat
```
- Kiểm tra xem đã có pip chưa:
```
pip list
```
- Vào lại CMD hoặc Git Bash, ta gõ lệnh này để tải thư viện BeautifulSoup4
```
pip install beautifulsoup4
pip install requests
```
- Tải xong ta vào trình duyệt code, ta tạo file đuôi .ipynb, bấm Select Kernal => Python Environments => venv
- Khi gõ những dòng lệnh này sẽ yêu cầu ipykernal package, bấm Install để tiếp tục
```python
import requests
from bs4 import BeautifulSoup
```
- Vào trang web cần cào dữ liệu, ta copy url và thực hiện request:
```python
url = "https://www.formula1.com/en/results/2024/drivers"
response = request.get(url)
```
```python
print(response)
```
Ở đây sẽ sẽ in ra request server trang web F1 là 200.

Ta sẽ thực hiện câu lệnh này:
```python
if response.status_code == 200:
    soup = BeautifulSoup(response.content, 'html.parser')
```
Ta được biến soup với type BeautifulSoup

- Ta có thể kiểm tra 1 số thông tin với biến Soup như sau:
```python
print(soup.title.text)
```
Ta sẽ được dòng title với text "2024 DRIVERS STANDING"

Hay
```python
print(soup.tag-name)
```
Để in ra các dòng có <tag-name> trong HTML
```python
print(soup.find('tag-name', class_= 'class-name'))
```
- Đề bài yêu cầu chính là cào dữ liệu bảng xếp hạng, ta sẽ inspect trang web và tìm class của table. Ta được kết quả class = "resultarchive-table". 

Từ đó ta sẽ sử dụng câu lệnh trên cũng như đặt biến và in ra để có thể in ra bảng trong html:
```python
table = soup.find('div', class_= 'resultarchive-table')
print(table)
```
- Sau đó ta bắt đầu tim tất cả tag tr trong bảng:
```python
rows = table.find_all('tr')
print(rows[1])
```
Từ đây sẽ in ra tên của tuyển thủ số 1 trong bảng xếp hạng tay đua dưới dạng HTML.
- Tiếp tục, ta sẽ in ra các row:
```python
    for row_id, row in enumerate(rows):
        columns = row.find('td')
        print(f"row={row_id}: {columns}")
```
Ta được row = 0 là NONE, còn lại là row = 1 -> n có tag td.
- Ta muốn in ra các row có columns, ta sẽ dùng điều kiện:
```python
for row_id, row in enumerate(rows)
    columns = row.find_all('td')
    if columns:
        print(columns)
```
Đồng thời sẽ dùng find_all để tìm hết các columns
- Giờ chúng ta sẽ in ra từng column một bằng cách sử dụng:
```python
if columns:
    position = columns[0].text.strip()
    driver_name = columns[1].text.strip().split()
    print(position, driver_name)
```
Sẽ in ra:
```
1 Max Verstappen VER
```
Như ở trong HTML.

Để có thể tách ra, ta sẽ đổi thành:
```python
driver_name = columns[1].text.strip().split('\n')
```
Ta được thành list:
```
1 ['Max', 'Verstappen', 'VER']
```
Sau đó ta sẽ:
```python
driver_name = columns[1].text.strip().split()
driver_name = ' '.join(driver_name[:-1])
```
Nhằm mất đi "VER"

Ta được:
```
1 Max Verstappen
```
Nếu để như thế này chắc chắn sẽ rất khó để nhìn, ta sẽ:
```python
print(f"Position: {position}\
        \nDriver Name: {driver_name}")
break
```
Từ đó ta được 
```
Position: 1
Driver Name: Max Verstappen
```
Tương tự với Nationality cũng như Car,...
### Chương trình Python
```python
import requests
from bs4 import BeautifulSoup
```
```python
url = 'https://www.formula1.com/en/results.html/2024/drivers.html'
response = requests.get(url)
```
```python
if response.status_code == 200:
    soup = BeautifulSoup(response.content, 'html.parser')
    table = soup.find('table', class_='f1-table f1-table-with-data w-full')
    rows = table.find_all('tr')
    
    for row_id, row in enumerate(rows):
        columns = row.find_all('td')
        if columns:
            position = columns[0].text.strip()
            driver_name = columns[1].text.strip().split()
            driver_name = ' '.join(driver_name[:-1])
            nationality = columns[2].text.strip()
            car = columns[3].text.strip()
            pts = columns[4].text.strip()
            print(f"Position: {position}\
                    \nDriver Name: {driver_name}\
                    \nNationality: {nationality}\
                    \nCar: {car}\
                    \nPoints: {pts}\n\n")
```
## Kết luận
Hy vọng qua bài báo cáo đầu tiên của tôi sẽ giúp bạn hiểu được định nghĩa của việc cào dữ liệu, cũng như ứng dụng và các công cụ của nó thông qua Demo sử dụng thư viện BeautifulSoup4 của Python được trình bày rõ ràng chi tiết.
## Tài liệu tham khảo
1. https://www.formula1.com/en/results/2024/drivers
2. https://tienziven.com/seo/crawling-la-gi/
3. https://pypi.org/project/beautifulsoup4/
