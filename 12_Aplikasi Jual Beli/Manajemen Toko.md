<h2 align="center"><strong>APLIKASI SOSIAL MEDIA</strong></h2>
</p>

<br>

<p align="center">
  <strong> ANGGOTA KELOMPOK 10:</strong><br>
  Haifa Zahra Azzimmi (2311102163)<br>
  Fadilah Salehah (2311102164)<br>
  Priesty Ameiliana Maulidah (2311102175)<br>
  S1 IF 11 05

### Source Code Program: 
```go
package main

import (
	"bufio"
	"fmt"
	"os"
	"strconv"
)

// Struktur data untuk barang FADILAH
type Item struct {
	id          int
	name        string
	category    string
	stock       int
	buyPrice    float64
	sellPrice   float64
	soldCount   int
	description string
	supplier    string
	minStock    int
}

// Struktur data untuk transaksi FADILAH
type Transaction struct {
	id            int
	itemId        int
	quantity      int
	date          string
	totalPrice    float64
	customerName  string
	paymentMethod string
}

// Variabel global untuk menyimpan data FADILAH
var items [100]Item
var transactions [100]Transaction
var itemCount, transactionCount int

// Function utama program FADILAH
func main() {
	scanner := bufio.NewScanner(os.Stdin)
	for {
		displayMenu()
		fmt.Print("Pilih menu: ")
		scanner.Scan()
		choice := scanner.Text()

		switch choice {
		case "1":
			tambahBarang(scanner)
		case "2":
			editBarang(scanner)
		case "3":
			deleteBarang(scanner)
		case "4":
			tambahTransaksi(scanner)
		case "5":
			editTransaction(scanner)
		case "6":
			deleteTransaction(scanner)
		case "7":
			displaySortedItems(scanner)
		case "8":
			searchItems(scanner)
		case "9":
			displayLaporanKeuangan()
		case "10":
			displayTopSellingItems()
		case "11":
			displayStokRendah()
		case "12":
			laporanPelanggan(scanner)
		case "0":
			return
		}
	}
}

// Function untuk menampilkan menu utama FADILAH
func displayMenu() {
	fmt.Println("\n=== SISTEM MANAJEMEN TOKO ===")
	fmt.Println("1. Tambah Barang")
	fmt.Println("2. Edit Barang")
	fmt.Println("3. Hapus Barang")
	fmt.Println("4. Tambah Transaksi")
	fmt.Println("5. Edit Transaksi")
	fmt.Println("6. Hapus Transaksi")
	fmt.Println("7. Tampilkan Barang Terurut")
	fmt.Println("8. Cari Barang")
	fmt.Println("9. Laporan Keuangan")
	fmt.Println("10. Top 5 Barang Terlaris")
	fmt.Println("11. Alert Stok Rendah")
	fmt.Println("12. Laporan Pelanggan")
	fmt.Println("0. Keluar")
}

// Function untuk menambahkan barang baru FADILAH
func tambahBarang(scanner *bufio.Scanner) {
	if itemCount >= 100 {
		fmt.Println("Penyimpanan barang penuh!")
		return
	}

	items[itemCount].id = itemCount + 1
	fmt.Print("Nama barang: ")
	scanner.Scan()
	items[itemCount].name = scanner.Text()

	fmt.Print("Kategori: ")
	scanner.Scan()
	items[itemCount].category = scanner.Text()

	fmt.Print("Stok: ")
	scanner.Scan()
	items[itemCount].stock, _ = strconv.Atoi(scanner.Text())

	fmt.Print("Harga beli: ")
	scanner.Scan()
	items[itemCount].buyPrice, _ = strconv.ParseFloat(scanner.Text(), 64)

	fmt.Print("Harga jual: ")
	scanner.Scan()
	items[itemCount].sellPrice, _ = strconv.ParseFloat(scanner.Text(), 64)

	fmt.Print("Deskripsi: ")
	scanner.Scan()
	items[itemCount].description = scanner.Text()

	fmt.Print("Supplier: ")
	scanner.Scan()
	items[itemCount].supplier = scanner.Text()

	fmt.Print("Minimum stok: ")
	scanner.Scan()
	items[itemCount].minStock, _ = strconv.Atoi(scanner.Text())

	itemCount++
	fmt.Println("Barang berhasil ditambahkan!")
}

// Function untuk mencari barang dengan Sequential Search FADILAH
func findItemById(id int) int {
	for i := 0; i < itemCount; i++ {
		if items[i].id == id {
			return i
		}
	}
	return -1
}

// Function untuk mengedit data barang ZAHRA
func editBarang(scanner *bufio.Scanner) {
	if itemCount == 0 {
		fmt.Println("Tidak ada barang yang tersedia untuk diedit!")
		return
	}

	fmt.Print("Masukkan ID barang yang akan diubah: ")
	scanner.Scan()
	id, err := strconv.Atoi(scanner.Text())
	if err != nil {
		fmt.Println("ID harus berupa angka!")
		return
	}

	found := false
	var idx int
	for i := 0; i < itemCount; i++ {
		if items[i].id == id {
			found = true
			idx = i
			break
		}
	}

	if !found {
		fmt.Println("Barang tidak ditemukan!")
		return
	}

	fmt.Print("Nama baru (kosongkan jika tidak diubah): ")
	scanner.Scan()
	input := scanner.Text()
	if input != "" {
		items[idx].name = input
	}

	fmt.Print("Kategori baru (kosongkan jika tidak diubah): ")
	scanner.Scan()
	input = scanner.Text()
	if input != "" {
		items[idx].category = input
	}

	fmt.Print("Stok baru (kosongkan jika tidak diubah): ")
	scanner.Scan()
	input = scanner.Text()
	if input != "" {
		stock, err := strconv.Atoi(input)
		if err == nil && validatePositiveNumber(stock) {
			items[idx].stock = stock
		} else {
			fmt.Println("Input tidak valid! Stok harus berupa angka positif.")
		}
	}

	fmt.Print("Harga beli baru (kosongkan jika tidak diubah): ")
	scanner.Scan()
	input = scanner.Text()
	if input != "" {
		buyPrice, err := strconv.ParseFloat(input, 64)
		if err == nil && validatePositiveFloat(buyPrice) {
			items[idx].buyPrice = buyPrice
		} else {
			fmt.Println("Input tidak valid! Harga beli harus berupa angka positif.")
		}
	}

	fmt.Print("Harga jual baru (kosongkan jika tidak diubah): ")
	scanner.Scan()
	input = scanner.Text()
	if input != "" {
		sellPrice, err := strconv.ParseFloat(input, 64)
		if err == nil && validatePositiveFloat(sellPrice) {
			items[idx].sellPrice = sellPrice
		} else {
			fmt.Println("Input tidak valid! Harga jual harus berupa angka positif.")
		}
	}

	fmt.Print("Deskripsi baru (kosongkan jika tidak diubah): ")
	scanner.Scan()
	input = scanner.Text()
	if input != "" {
		items[idx].description = input
	}

	fmt.Print("Supplier baru (kosongkan jika tidak diubah): ")
	scanner.Scan()
	input = scanner.Text()
	if input != "" {
		items[idx].supplier = input
	}

	fmt.Print("Minimum stok baru (kosongkan jika tidak diubah): ")
	scanner.Scan()
	input = scanner.Text()
	if input != "" {
		minStock, err := strconv.Atoi(input)
		if err == nil && validatePositiveNumber(minStock) {
			items[idx].minStock = minStock
		} else {
			fmt.Println("Input tidak valid! Minimum stok harus berupa angka positif.")
		}
	}

	fmt.Println("Data barang berhasil diubah!")
}

// Function untuk menghapus barang ZAHRA
func deleteBarang(scanner *bufio.Scanner) {
	if itemCount == 0 {
		fmt.Println("Tidak ada barang yang tersedia untuk dihapus!")
		return
	}

	fmt.Print("Masukkan ID barang yang akan dihapus: ")
	scanner.Scan()
	id, err := strconv.Atoi(scanner.Text())
	if err != nil {
		fmt.Println("ID harus berupa angka!")
		return
	}

	found := false
	var idx int
	for i := 0; i < itemCount; i++ {
		if items[i].id == id {
			found = true
			idx = i
			break
		}
	}

	if !found {
		fmt.Println("Barang tidak ditemukan!")
		return
	}

	for i := idx; i < itemCount-1; i++ {
		items[i] = items[i+1]
	}
	itemCount--
	fmt.Println("Barang berhasil dihapus!")
}

// Function untuk menambah transaksi ZAHRA
func tambahTransaksi(scanner *bufio.Scanner) {
	if itemCount == 0 {
		fmt.Println("Tidak ada barang yang tersedia untuk transaksi!")
		return
	}

	if transactionCount >= 100 {
		fmt.Println("Penyimpanan transaksi penuh!")
		return
	}

	fmt.Print("ID Barang: ")
	scanner.Scan()
	itemId, err := strconv.Atoi(scanner.Text())
	if err != nil {
		fmt.Println("ID harus berupa angka!")
		return
	}

	found := false
	var itemIdx int
	for i := 0; i < itemCount; i++ {
		if items[i].id == itemId {
			found = true
			itemIdx = i
			break
		}
	}

	if !found {
		fmt.Println("Barang tidak ditemukan!")
		return
	}

	fmt.Print("Jumlah: ")
	scanner.Scan()
	quantity, err := strconv.Atoi(scanner.Text())
	if err != nil || quantity <= 0 {
		fmt.Println("Jumlah harus berupa angka positif!")
		return
	}

	if quantity > items[itemIdx].stock {
		fmt.Println("Stok tidak mencukupi!")
		return
	}

	transactions[transactionCount].id = transactionCount + 1
	transactions[transactionCount].itemId = itemId
	transactions[transactionCount].quantity = quantity
	transactions[transactionCount].totalPrice = float64(quantity) * items[itemIdx].sellPrice

	fmt.Print("Nama pelanggan: ")
	scanner.Scan()
	transactions[transactionCount].customerName = scanner.Text()

	fmt.Print("Metode pembayaran: ")
	scanner.Scan()
	transactions[transactionCount].paymentMethod = scanner.Text()

	items[itemIdx].stock -= quantity
	items[itemIdx].soldCount += quantity

	transactionCount++
	fmt.Println("Transaksi berhasil ditambahkan!")
}

// Function untuk mengedit transaksi ZAHRA
func editTransaction(scanner *bufio.Scanner) {
	if transactionCount == 0 {
		fmt.Println("Tidak ada transaksi yang tersedia untuk diedit!")
		return
	}

	fmt.Print("Masukkan ID transaksi yang akan diubah: ")
	scanner.Scan()
	id, err := strconv.Atoi(scanner.Text())
	if err != nil {
		fmt.Println("ID harus berupa angka!")
		return
	}

	found := false
	var idx int
	for i := 0; i < transactionCount; i++ {
		if transactions[i].id == id {
			found = true
			idx = i
			break
		}
	}

	if !found {
		fmt.Println("Transaksi tidak ditemukan!")
		return
	}

	oldItemId := transactions[idx].itemId // Akan digunakan nanti
	oldQuantity := transactions[idx].quantity

	fmt.Print("ID Barang baru (kosongkan jika tidak diubah): ")
	scanner.Scan()
	input := scanner.Text()
	if input != "" {
		newItemId, err := strconv.Atoi(input)
		if err != nil {
			fmt.Println("ID harus berupa angka!")
			return
		}

		found := false
		for i := 0; i < itemCount; i++ {
			if items[i].id == newItemId {
				found = true
				// Kembalikan stok ke barang lama
				for j := 0; j < itemCount; j++ {
					if items[j].id == oldItemId {
						items[j].stock += oldQuantity
						items[j].soldCount -= oldQuantity
						break
					}
				}
				// Update stok barang baru
				items[i].stock -= transactions[idx].quantity
				items[i].soldCount += transactions[idx].quantity
				transactions[idx].itemId = newItemId
				transactions[idx].totalPrice = float64(transactions[idx].quantity) * items[i].sellPrice
				break
			}
		}

		if !found {
			fmt.Println("Barang tidak ditemukan!")
			return
		}
	}

	fmt.Print("Jumlah baru (kosongkan jika tidak diubah): ")
	scanner.Scan()
	input = scanner.Text()
	if input != "" {
		newQuantity, err := strconv.Atoi(input)
		if err != nil || newQuantity <= 0 {
			fmt.Println("Jumlah harus berupa angka positif!")
			return
		}

		var itemIdx int
		for i := 0; i < itemCount; i++ {
			if items[i].id == transactions[idx].itemId {
				itemIdx = i
				break
			}
		}

		adjustedStock := items[itemIdx].stock + oldQuantity
		if newQuantity > adjustedStock {
			fmt.Println("Stok tidak mencukupi!")
			return
		}

		items[itemIdx].stock = adjustedStock - newQuantity
		items[itemIdx].soldCount = items[itemIdx].soldCount - oldQuantity + newQuantity

		transactions[idx].quantity = newQuantity
		transactions[idx].totalPrice = float64(newQuantity) * items[itemIdx].sellPrice
	}

	fmt.Print("Nama pelanggan baru (kosongkan jika tidak diubah): ")
	scanner.Scan()
	input = scanner.Text()
	if input != "" {
		transactions[idx].customerName = input
	}

	fmt.Print("Metode pembayaran baru (kosongkan jika tidak diubah): ")
	scanner.Scan()
	input = scanner.Text()
	if input != "" {
		transactions[idx].paymentMethod = input
	}

	fmt.Println("Transaksi berhasil diubah!")
}

// Function untuk menghapus transaksi ZAHRA
func deleteTransaction(scanner *bufio.Scanner) {
	if transactionCount == 0 {
		fmt.Println("Tidak ada transaksi yang tersedia untuk dihapus!")
		return
	}

	fmt.Print("Masukkan ID transaksi yang akan dihapus: ")
	scanner.Scan()
	id, err := strconv.Atoi(scanner.Text())
	if err != nil {
		fmt.Println("ID harus berupa angka!")
		return
	}

	found := false
	var idx int
	for i := 0; i < transactionCount; i++ {
		if transactions[i].id == id {
			found = true
			idx = i
			break
		}
	}

	if !found {
		fmt.Println("Transaksi tidak ditemukan!")
		return
	}

	var itemIdx int
	for i := 0; i < itemCount; i++ {
		if items[i].id == transactions[idx].itemId {
			itemIdx = i
			break
		}
	}

	items[itemIdx].stock += transactions[idx].quantity
	items[itemIdx].soldCount -= transactions[idx].quantity

	for i := idx; i < transactionCount-1; i++ {
		transactions[i] = transactions[i+1]
	}
	transactionCount--
	fmt.Println("Transaksi berhasil dihapus!")
}

// Tambahan validasi untuk input angka negatif
func validatePositiveNumber(value int) bool {
	return value >= 0
}

func validatePositiveFloat(value float64) bool {
	return value >= 0.0
}

// Function untuk Selection Sort ZAHRA
func selectionSort(arr [100]Item, count int, field string, ascending bool) [100]Item {
	for i := 0; i < count-1; i++ {
		minIdx := i
		for j := i + 1; j < count; j++ {
			compare := false
			switch field {
			case "name":
				if ascending {
					compare = arr[j].name < arr[minIdx].name
				} else {
					compare = arr[j].name > arr[minIdx].name
				}
			case "price":
				if ascending {
					compare = arr[j].sellPrice < arr[minIdx].sellPrice
				} else {
					compare = arr[j].sellPrice > arr[minIdx].sellPrice
				}
			}
			if compare {
				minIdx = j
			}
		}
		temp := arr[i]
		arr[i] = arr[minIdx]
		arr[minIdx] = temp
	}
	return arr
}

// Function untuk menampilkan alert stok rendah PRIESTY
func displayStokRendah() {
	fmt.Println("\n=== ALERT STOK RENDAH ===")
	found := false
	for i := 0; i < itemCount; i++ {
		if items[i].stock <= items[i].minStock {
			fmt.Printf("PERINGATAN: %s (ID: %d) memiliki stok rendah (%d)\n",
				items[i].name, items[i].id, items[i].stock)
			found = true
		}
	}
	if !found {
		fmt.Println("Tidak ada barang dengan stok rendah")
	}
}

// Function untuk generate laporan pelanggan PRIESTY
func laporanPelanggan(scanner *bufio.Scanner) {
	fmt.Print("Masukkan nama pelanggan: ")
	scanner.Scan()
	customerName := scanner.Text()

	fmt.Printf("\n=== LAPORAN PEMBELIAN PELANGGAN: %s ===\n", customerName)
	totalSpent := 0.0
	for i := 0; i < transactionCount; i++ {
		if transactions[i].customerName == customerName {
			itemIdx := findItemById(transactions[i].itemId)
			fmt.Printf("Transaksi #%d: %s (Qty: %d) - Total: Rp%.2f\n",
				transactions[i].id,
				items[itemIdx].name,
				transactions[i].quantity,
				transactions[i].totalPrice)
			totalSpent += transactions[i].totalPrice
		}
	}
	fmt.Printf("\nTotal pembelian: Rp%.2f\n", totalSpent)
}

// Function untuk Binary Search PRIESTY
func binarySearch(arr [100]Item, count int, key string) int {
	left := 0
	right := count - 1

	for left <= right {
		mid := (left + right) / 2
		if arr[mid].name == key {
			return mid
		}
		if arr[mid].name < key {
			left = mid + 1
		} else {
			right = mid - 1
		}
	}
	return -1
}

func searchItems(scanner *bufio.Scanner) {
	fmt.Print("Masukkan kata kunci pencarian: ")
	scanner.Scan()
	keyword := scanner.Text()

	// Sorting array untuk binary search
	items = selectionSort(items, itemCount, "name", true)

	// Melakukan binary search
	idx := binarySearch(items, itemCount, keyword)
	if idx != -1 {
		fmt.Printf("\nBarang ditemukan:\n")
		fmt.Printf("ID: %d\nNama: %s\nKategori: %s\nStok: %d\nHarga: Rp%.2f\n",
			items[idx].id,
			items[idx].name,
			items[idx].category,
			items[idx].stock,
			items[idx].sellPrice)
	} else {
		fmt.Println("Barang tidak ditemukan!")
	}
}

// Function untuk menampilkan laporan keuangan PRIESTY
func displayLaporanKeuangan() {
	var totalRevenue, totalCost, profit float64

	for i := 0; i < transactionCount; i++ {
		itemIdx := findItemById(transactions[i].itemId)
		totalRevenue += transactions[i].totalPrice
		totalCost += items[itemIdx].buyPrice * float64(transactions[i].quantity)
	}

	profit = totalRevenue - totalCost

	fmt.Println("\n=== LAPORAN KEUANGAN ===")
	fmt.Printf("Total Pendapatan: Rp%.2f\n", totalRevenue)
	fmt.Printf("Total Modal: Rp%.2f\n", totalCost)
	fmt.Printf("Keuntungan: Rp%.2f\n", profit)
}

// Function untuk menampilkan top 5 barang terlaris PRIESTY
func displayTopSellingItems() {
	if itemCount == 0 {
		fmt.Println("Tidak ada barang yang tersedia untuk ditampilkan!")
		return
	}

	// Buat salinan array untuk sorting
	var sortedItems [100]Item
	copy(sortedItems[:], items[:])

	// Sort berdasarkan soldCount (descending)
	for i := 0; i < itemCount-1; i++ {
		maxIdx := i
		for j := i + 1; j < itemCount; j++ {
			if sortedItems[j].soldCount > sortedItems[maxIdx].soldCount {
				maxIdx = j
			}
		}
		temp := sortedItems[i]
		sortedItems[i] = sortedItems[maxIdx]
		sortedItems[maxIdx] = temp
	}

	fmt.Println("\n=== TOP 5 BARANG TERLARIS ===")
	limit := 5
	if itemCount < 5 {
		limit = itemCount
	}

	for i := 0; i < limit; i++ {
		fmt.Printf("%d. %s (Terjual: %d)\n",
			i+1,
			sortedItems[i].name,
			sortedItems[i].soldCount)
	}
}

func displaySortedItems(scanner *bufio.Scanner) {
	if itemCount == 0 {
		fmt.Println("Tidak ada barang untuk ditampilkan!")
		return
	}

	fmt.Println("\nPilih urutan:")
	fmt.Println("1. Nama (Ascending)")
	fmt.Println("2. Nama (Descending)")
	fmt.Println("3. Harga (Ascending)")
	fmt.Println("4. Harga (Descending)")
	fmt.Print("Pilihan Anda: ")
	scanner.Scan()
	choice := scanner.Text()

	// Buat salinan array untuk sorting
	var sortedItems [100]Item
	copy(sortedItems[:], items[:])

	// Lakukan sorting berdasarkan pilihan
	switch choice {
	case "1":
		sortedItems = selectionSort(sortedItems, itemCount, "name", true)
	case "2":
		sortedItems = selectionSort(sortedItems, itemCount, "name", false)
	case "3":
		sortedItems = selectionSort(sortedItems, itemCount, "price", true)
	case "4":
		sortedItems = selectionSort(sortedItems, itemCount, "price", false)
	default:
		fmt.Println("Pilihan tidak valid!")
		return
	}

	// Tampilkan hasil sorting PRIESTY
	fmt.Println("\n=== DAFTAR BARANG TERURUT ===")
	for i := 0; i < itemCount; i++ {
		fmt.Printf("ID: %d, Nama: %s, Kategori: %s, Stok: %d, Harga: Rp%.2f\n",
			sortedItems[i].id, sortedItems[i].name, sortedItems[i].category,
			sortedItems[i].stock, sortedItems[i].sellPrice)
	}
}

```
