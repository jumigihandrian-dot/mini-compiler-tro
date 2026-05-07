# Mini Compiler - Operator Pangkat (^)

## Nama Tugas
Implementasi Mini Compiler dengan dukungan operator pangkat (`^`) menggunakan:

- Lexical Analysis
- EBNF
- Abstract Syntax Tree (AST)
- Three Address Code (TAC)

# =========================
# UJI COBA
# =========================

source_code = "a ^ 2 + b * c"

symbol_table = {
    'a': 5,
    'b': 10,
    'c': 2
}

# Screenshot Program

## Hasil Running Program

<p align="center">
  <img src="images/Screenshot 2026-05-08 000036.png" width="800">
</p>

try:
    print(f"Input: {source_code}")

    compiler = MiniCompiler(source_code, symbol_table)

    ast_root = compiler.expr()

    print("\n--- Output Three Address Code (TAC) ---")

    compiler.generate_tac(ast_root)

except Exception as e:
    print(f"Error: {e}")
```

---

# Hasil Output

```text
Input: a ^ 2 + b * c

--- Output Three Address Code (TAC) ---
t1 = a ^ 2
t2 = b * c
t3 = t1 + t2
```

# Jawaban Pertanyaan Refleksi

## 1. Mengapa fungsi `power()` harus dipanggil di dalam `term()`, bukan sebaliknya?

Karena operator pangkat (`^`) memiliki prioritas lebih tinggi dibanding operator perkalian (`*`) dan pembagian (`/`).

Urutan prioritas operator matematika:

1. Kurung `()`
2. Pangkat `^`
3. Kali/Bagi `* /`
4. Tambah/Kurang `+ -`

Dengan memanggil `power()` di dalam `term()`, maka operasi pangkat akan diproses terlebih dahulu sebelum operasi perkalian atau pembagian.

Contoh:

```text
a ^ 2 * b
```

Diproses menjadi:

```text
(a ^ 2) * b
```

---

## 2. Apa yang terjadi jika variabel `z` digunakan tetapi tidak ada di `symbol_table`?

Compiler akan menghasilkan Semantic Error karena variabel tersebut belum didefinisikan.

Contoh:

```python
source_code = "z + 5"
```

Jika:

```python
symbol_table = {}
```

Maka muncul error:

```text
Semantic Error: Undefined variable 'z'
```

Hal ini terjadi pada fase Analisis Semantik.

---

## 3. Mengapa instruksi `a ^ 2` harus muncul sebelum instruksi `+` pada TAC?

Karena TAC mengikuti urutan evaluasi berdasarkan prioritas operator.

Pada ekspresi:

```text
a ^ 2 + b * c
```

Operasi pangkat harus dihitung terlebih dahulu sebelum penjumlahan.

Urutan evaluasi:

1. `a ^ 2`
2. `b * c`
3. hasil dijumlahkan

Sehingga TAC menjadi:

```text
t1 = a ^ 2
t2 = b * c
t3 = t1 + t2
```

Hal ini memastikan hasil perhitungan sesuai aturan matematika.

---

# Kesimpulan

Mini Compiler berhasil dikembangkan dengan menambahkan dukungan operator pangkat (`^`).

Perubahan dilakukan pada:

- Lexical Analysis
- Parser
- Operator Precedence
- Three Address Code (TAC)

Program berhasil menghasilkan AST dan TAC sesuai aturan matematika dan operator precedence.
