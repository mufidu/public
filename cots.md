# latihan
tampilkan jumlah karyawan per job title
```sql
SELECT jobTitle, COUNT(employeeNumber) AS jumlahKaryawan 
FROM employees 
GROUP BY jobTitle
```

tampilkan informasi nama employee dan nama atasan dari employee
```sql
SELECT CONCAT(e1.firstName, " ", e1.lastName) AS fullName, CONCAT(e2.firstName, " ", e2.lastName) AS atasan 
FROM employees as e1 
LEFT JOIN employees as e2 ON e1.reportsTo = e2.employeeNumber
```

tampilkan first name dan last name karyawan dan berikan inisial sebagai "Nama" untuk karyawan yang memiliki job title = 'Sales Rep'
```sql
SELECT CONCAT(firstName, " ", lastName) AS nama 
FROM employees WHERE jobTitle = "Sales Rep"
```

tampilkan total pembayaran pada tabel payment berdasarkan tahun serta urutkan berdasarkan tahun terkecil
```sql
SELECT SUM(amount) AS total FROM payments ORDER BY paymentDate ASC
```

tampilkan informasi nama customer dan jumlah order di goup berdasarkan tahun order untuk tahun order=2005
```sql
SELECT customerName, COUNT(orders.orderNumber) AS jumlahOrder 
FROM customers 
JOIN orders ON customers.customerNumber = orders.customerNumber 
WHERE YEAR(orders.orderDate) = 2005 
GROUP BY orders.orderDate
```

tampilkan first name dan last name dari nama karyawan yang memiliki atasan dengan Anthony Bow
```sql
select concat(e1.firstName, " ", e1.lastName) as namaKaryawan
from employees e1
join employees e2
on e1.reportsTo = e2.employeeNumber
where e2.firstName = "Anthony" and e2.lastName = "Bow";
```

tampilkan total pembayaran pada tabel payment berdasarkan tahun dan bulan untuk payment pada tahun 2003
```sql
SELECT *, COUNT(amount) AS total 
FROM payments 
WHERE YEAR(paymentDate) = 2003 
GROUP BY YEAR(paymentDate), MONTH(paymentDate)  
```

tampilkan jumlah order per tanggal order (tahun) dengan status pengiriman = 'Shipped'
```sql
SELECT COUNT(orderNumber) AS jumlahOrder 
FROM orders WHERE status = 'Shipped' 
GROUP BY YEAR(orderDate)
```

tampilkan jumlah order per tanggal order (tahun) dengan status pengiriman selain 'Shipped'
```sql
SELECT COUNT(orderNumber) AS jumOrder 
FROM orders 
WHERE NOT status = 'Shipped' 
GROUP BY YEAR(orderDate)
```

# Responsi 4
Tampilkan nama customer dari data customer dimana credit limitnya 0.00 dan diawali dengan huruf s
```sql
SELECT customerName 
FROM customers 
WHERE creditLimit NOT IN (0.00) AND customerName LIKE 'S%';
```

Tampilkan nama lengkap contact, city dan country dari data customer dimana credit limitnya lebih besar dari 21000 dan postalcodenya bernomor 44000
```sql
SET sql_mode = PIPES_AS_CONCAT;
SELECT contactFirstName || contactLastName AS contact, city, country 
FROM customers 
WHERE creditLimit > 21000 AND postalCode = 44000;
```

Tampilkan productCode, productLine, dan productVendor dari data products dimana stock quantitynya jika dibagi 2 harus lebih besar sama dengan dari 4000 dan untuk buyPrice atau MSRP nya jika dikalikan 5% dan 2% harus lebih besar dari 2.0 dan lebih kecil dari 4.0
```sql
SELECT productCode, productLine, productVendor 
FROM products 
WHERE quantityInStock / 2 >= 4000 AND buyPrice * (5 / 100) > 2.0 OR MSRP * (2 / 100) < 4.0;
```

Tampilkan nama lengkap employee dan jobtitlenya dari data employees dimana officecodenya 4 dan 6 dan report to-nya selain 1002 dan 1088 dan tampilan terurut dari kecil ke besar berdasarkan nama lengkap employee
```sql
SET sql_mode = PIPES_AS_CONCAT;
SELECT firstName || lastName AS EmployeeName, jobTitle 
FROM employees 
WHERE officeCode IN ('4','6') AND reportsTo NOT IN (1002,1088) 
ORDER BY EmployeeName ASC;
```

Tampilkan customerNumber, checkNumber dan paymentDate pada data payments dimana amount tidak diantara nilai 500 sampai 100000 dan amout dikalikan 10% hasilnya tidak dengan 12016.658 dan tampilan terurut dari besar ke kecil berdasarkan paymentDate 
```sql
SELECT customerNumber, checkNumber, paymentDate 
FROM payments 
WHERE amount NOT BETWEEN 500 AND 100000 AND amount * (10 / 100) <> 12016.658 
ORDER BY paymentDate DESC;
```

# Responsi 5
Tampilkan 5 nama customer dan total limit cerditnya yang berasal dari tabel customers dimana limit creditnya diatas 35000 dimana tampilan data dikelompokkan berdasarkan customer name  dan data terurut berdasarkan total limit kreditnya dari terbesar ke terkecil.
```sql
SELECT customerName, SUM(creditLimit) AS "Total Limit Credit" 
FROM customers
WHERE creditLimit > 35000
GROUP BY customerName
ORDER BY SUM(creditLimit) DESC
LIMIT 5;
```

Tampilkan jabatan dan banyak jabatan yang ada pada tabel employees yang diurutkan berdasarkan jabatannya dari terbesar ke terkecil
```sql
SELECT jobTitle, COUNT(jobTitle) AS "Banyak"
FROM employees
GROUP BY jobTitle
ORDER BY jobTitle DESC;
```

Tampilkan nomor customer, banyak nomor check, tanggal pembayaran, dan total amonut dari tabel payments dimana tanggal pembayarannya lebih dari 19 Oktober 2004 serta banyak nomor checknya lebih dari 3 dan total amountnya lebih dari 25000 dikelompokan dan diurutkan berdasarkan nomor customer
```sql
SELECT customerNumber, COUNT(checkNumber) AS "banyak checkNumber", paymentDate, SUM(amount) AS "total amount"
FROM payments
WHERE paymentDate > '2004-10-19'
GROUP BY customerNumber
HAVING COUNT(checkNumber) > 2 AND SUM(amount) >= 25000
ORDER BY customerNumber;
```

Tampilkan 5 nama product, buyprice dan jumlah buyprice dikalikan quantityInstock yang dibulatkan ke atas jika desimal sebagai total dimana nama produknya memiliki angka 19 didepannya dan total lebih besar dari total dibagi akar 1000 dikategorikan  dan diurutkanberdasarkan nama produk dari terbesar ke terkecil.
```sql
SELECT productName, buyPrice, CEIL(SUM(buyPrice*quantityInStock)) AS "Total"
FROM products
WHERE productName LIKE '19%'
GROUP BY productName
HAVING SUM(buyPrice*quantityInStock) > SUM(buyPrice*quantityInStock)/SQRT(1000)
ORDER BY productName DESC
LIMIT 5;
```

Tampilkan country, addressLine1 dalam huruf besar, addressLine2 dalam huruf kecil, dan panjang karakter anddressLine 1 dan 2 disertai spasi yang addressLine2 dan statenya tidak ada data NULL
```sql
SELECT country, UPPER(addressLine1) AS "addressLine1", LOWER(addressLine2) AS "addressLine2" , LENGTH(CONCAT(addressLine1,"",addressLine2)) AS "panjang karakter alamat 1 & 2"
FROM offices
WHERE addressLine2 IS NOT NULL AND state IS NOT NULL;
```

# Responsi 6
Tampilkan nama customer, nama employee dan bidang pekerjaanya jika officodenya lebih dari 1 dan country dari customer adalah USA. Urutkan dari terkecil ke terbesar dan batasi hanya lima data saja yang muncul.
```sql
SELECT c.customerName, CONCAT(e.firstName, e.lastName) AS "employeeName", e.jobTitle
FROM customers c
JOIN employees e 
ON c.salesRepEmployeeNumber = e.employeeNumber
WHERE e.officeCode > 1 AND c.country = 'USA'
ORDER BY customerName
LIMIT 5;
```

Tampilkan productLine, productName dan quantityOrdered dimana quantityInStock lebih besar sama dengan 3500 dan jumlah dari priceEach lebih besar dari 100.00 dimana data dikelompokkan dan diurutkan berdasarkan productLine dari terbesar ke terkecil.
```sql
SELECT pl.productLine, p.productName, od.quantityOrdered
FROM productlines pl
JOIN products p USING (productLine)
JOIN orderdetails od USING (productCode)
WHERE p.quantityInStock >= 3500
GROUP BY pl.productLine
HAVING SUM(od.priceEach) > 100.00
ORDER BY pl.productLine DESC;
```

Tampilkan item minimum, item maksimum dan rata-rata item yang dibulatkan ke atas yang berasal dari tabel lineitems yang diproses dari orderNumber, banyak orderNumber dialiaskan items yang berasal dari tabel orderdetails yang digrupkan berdasarkan orderNumber 
```sql
SELECT MAX(items), MIN(items), CEIL(AVG(items))
FROM (SELECT orderNumber, COUNT(orderNumber) AS items
	  FROM orderdetails
	  GROUP BY orderNumber) AS lineitems;
```

Tampilkan nama customes dari tabel customer yang dimana customer numbernya tidak termasuk dalam customer number pada tabel orders.
```sql
SELECT customerName
FROM customers
WHERE customerNumber NOT IN (SELECT DISTINCT customerNumber
			     FROM orders);
```

Tampilkan customer number dan customer name  dari tabel customers dimana kebenaran (EXISTS) bahwa orderNumber dan jumlah dari priceEach dikalikan quantityOrdered dimana jumlahnya tersebut lebih besar dari 60000 dari tabel orderdetails yang dihubungkan secara mendalam dengan tabel orders dimana customer number harus sama dengan customers number dari tabel customers yang dikategorikan dengan orderNumber. (hint: pada WHERE gunakan EXISTS)
```sql
SELECT customerNumber, customerName
FROM customers
WHERE EXISTS(SELECT orderNumber, SUM(priceEach * quantityOrdered)
	     FROM orderdetails
	     INNER JOIN orders USING (orderNumber)
   	     WHERE customerNumber = customers.customerNumber
	     GROUP BY orderNumber
	     HAVING SUM(priceEach * quantityOrdered) > 60000);
```





