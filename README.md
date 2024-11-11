# Tugas 6: Aplikasi Cek Cuaca Sederhana

### Pembuat
- **Nama**: Ferdhyan Dwi Rangga Saputra
- **NPM**: 2210010461

---

## 1. Deskripsi Program
Aplikasi ini memungkinkan pengguna untuk:
- Mengambil informasi cuaca secara real-time untuk kota yang dipilih atau dimasukkan.
- Menampilkan data cuaca seperti deskripsi cuaca dan suhu untuk lokasi yang dipilih.
- Menyimpan data cuaca dalam format CSV untuk digunakan di masa mendatang.

## 2. Komponen GUI
- **JFrame**: Window utama aplikasi.
- **JPanel**: Panel untuk menampung komponen.
- **JLabel**: Label untuk menampilkan informasi cuaca.
- **JTextField**: Input untuk memasukkan nama kota.
- **JButton**: Tombol untuk memeriksa dan menyimpan cuaca.
- **JComboBox**: Dropdown untuk memilih kota dari daftar favorit.
- **JTable**: Tabel untuk menampilkan riwayat data cuaca.

## 3. Logika Program
- Menggunakan API eksternal **OpenWeatherMap** untuk mengambil data cuaca real-time.
- Menyimpan daftar kota favorit dalam file teks agar dapat dimuat kembali.
- Menyimpan data cuaca ke dalam file CSV, sehingga pengguna dapat melihat data cuaca yang tersimpan di masa lalu.

## 4. Events
Menggunakan **ActionListener** dan **ItemListener** untuk menangani interaksi pengguna:

### A. Tombol Cek Cuaca
Mengambil data cuaca berdasarkan nama kota yang dimasukkan dan menampilkan informasi cuaca pada aplikasi.

```java
private void cekCuacaActionPerformed(ActionEvent evt) {
        String apiKey = "528c4ceb36aaecefd267e3ce8129ca25"; // Ganti dengan API key OpenWeatherMap
        String kota = txtCari.getText().trim();
        
        if (!kota.isEmpty()) {
            JSONObject cuacaData = ambilDataCuaca(apiKey, kota);
            if (cuacaData != null) {
                tampilkanDataCuaca(cuacaData, kota);
            } else {
                JOptionPane.showMessageDialog(this, "Kota tidak ditemukan!", "Error", JOptionPane.ERROR_MESSAGE);
            }
        }
    }
```

### B. ItemListener pada JComboBox
Mengambil data cuaca untuk kota yang dipilih dari **JComboBox** dan menampilkannya di aplikasi.

```java
// Event handler untuk perubahan item pada JComboBox
        cbKota.addItemListener(new ItemListener() {
            public void itemStateChanged(ItemEvent evt) {
                if (evt.getStateChange() == ItemEvent.SELECTED) {
                    txtCari.setText((String) cbKota.getSelectedItem());
                }
            }
        });
``` 


## 5. Variasi
Aplikasi ini memiliki variasi tambahan berikut:

### A. Daftar Kota Favorit
Pengguna dapat menyimpan kota yang sering dicek sebagai daftar favorit yang dapat diakses dari **JComboBox**.

```java
private void loadLokasiFavorit() {
        cbKota.removeAllItems();
        for (String kota : lokasiFavorit) {
            cbKota.addItem(kota);
        }
    }
```
 
### B. Tombol untuk Menyimpan Data dari Tabel ke Dalam File CSV
Aplikasi menyimpan data cuaca dalam format CSV

```java
private void simpanDataCuaca() {
        try (FileWriter writer = new FileWriter("data_cuaca.csv")) {
            for (int i = 0; i < tableModel.getRowCount(); i++) {
                writer.write(tableModel.getValueAt(i, 0) + "," + tableModel.getValueAt(i, 1) + "," + tableModel.getValueAt(i, 2) + "\n");
            }
            writer.flush();
            JOptionPane.showMessageDialog(this, "Data cuaca berhasil disimpan ke data_cuaca.csv");
        } catch (IOException e) {
            JOptionPane.showMessageDialog(this, "Error: " + e.getMessage(), "Error", JOptionPane.ERROR_MESSAGE);
        }
    }
```

### C. Tombol untuk Memuat data
Fitur untuk Memuat Data Cuaca yang Tersimpan dan Menampilkannya di JTable

```java
private void muatDataCuaca() {
        try (BufferedReader reader = new BufferedReader(new FileReader("data_cuaca.csv"))) {
            String line;
            tableModel.setRowCount(0);
            while ((line = reader.readLine()) != null) {
                String[] data = line.split(",");
                tableModel.addRow(data);
            }
            JOptionPane.showMessageDialog(this, "Data cuaca berhasil dimuat dari data_cuaca.csv");
        } catch (IOException e) {
            JOptionPane.showMessageDialog(this, "Error: " + e.getMessage(), "Error", JOptionPane.ERROR_MESSAGE);
        }
    }
``` 


## 6. Tampilan Pada Saat Aplikasi Di Jalankan



## 7. Indikator Penilaian

| No  | Komponen          | Persentase |
| :-: | ------------------ | :--------: |
|  1  | Komponen GUI      |     10%    |
|  2  | Logika Program    |     20%    |
|  3  | Events            |     10%    |
|  4  | Kesesuaian UI     |     20%    |
|  5  | Memenuhi Variasi  |     40%    |
|     | **TOTAL**         |  **100%**  |

--- 
