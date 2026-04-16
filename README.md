# Finance-App
"use client";
import { useState } from "react";

export default function Home() {
  const [data, setData] = useState({
    jenis: "pengeluaran",
    nominal: "",
    keterangan: "",
  });

  const [list, setList] = useState([]);

  const handleSubmit = (e) => {
    e.preventDefault();
    setList([...list, data]);
    setData({ jenis: "pengeluaran", nominal: "", keterangan: "" });
  };

  const total = list.reduce((acc, item) => {
    return item.jenis === "pemasukan"
      ? acc + Number(item.nominal)
      : acc - Number(item.nominal);
  }, 0);

  return (
    <div style={{ padding: 20 }}>
      <h1>Finance App</h1>

      <h2>Saldo: Rp {total}</h2>

      <form onSubmit={handleSubmit}>
        <select
          value={data.jenis}
          onChange={(e) => setData({ ...data, jenis: e.target.value })}
        >
          <option value="pengeluaran">Pengeluaran</option>
          <option value="pemasukan">Pemasukan</option>
        </select>
        <br /><br />

        <input
          type="number"
          placeholder="Nominal"
          value={data.nominal}
          onChange={(e) => setData({ ...data, nominal: e.target.value })}
        />
        <br /><br />

        <input
          placeholder="Keterangan"
          value={data.keterangan}
          onChange={(e) => setData({ ...data, keterangan: e.target.value })}
        />
        <br /><br />

        <button type="submit">Tambah</button>
      </form>

      <hr />

      <h3>History</h3>
      {list.map((item, i) => (
        <div key={i}>
          {item.jenis} - Rp {item.nominal} ({item.keterangan})
        </div>
      ))}
    </div>
  );
}
