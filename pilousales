// App.jsx — Version complète avec ADMIN (ajout / modification / suppression)
// Fonctionne avec React + Tailwind
// Copie-colle dans src/App.jsx

import React, { useState, useEffect } from 'react';

export default function App() {
  const [products, setProducts] = useState(() => {
    const saved = localStorage.getItem("products");
    return saved ? JSON.parse(saved) : [
      {
        id: 1,
        title: "Casque Bluetooth SuperSound",
        price: "39.99 €",
        description: "Casque Bluetooth léger, autonomie 24h, réduction du bruit.",
        image: "https://via.placeholder.com/320x200?text=Casque",
        affiliate_url: "https://example.com/casque"
      }
    ];
  });

  const [adminMode, setAdminMode] = useState(false);
  const [editItem, setEditItem] = useState(null);
  const [selected, setSelected] = useState(null);
  const [query, setQuery] = useState("");

  const emptyForm = { id: null, title: "", price: "", description: "", image: "", affiliate_url: "" };
  const [form, setForm] = useState(emptyForm);

  useEffect(() => {
    localStorage.setItem("products", JSON.stringify(products));
  }, [products]);

  const filtered = products.filter(p =>
    p.title.toLowerCase().includes(query.toLowerCase()) ||
    p.description.toLowerCase().includes(query.toLowerCase())
  );

  const handleSubmit = (e) => {
    e.preventDefault();

    if (form.id) {
      setProducts(products.map(p => p.id === form.id ? form : p));
    } else {
      setProducts([...products, { ...form, id: Date.now() }]);
    }

    setForm(emptyForm);
    setEditItem(null);
  };

  const handleEdit = (product) => {
    setForm(product);
    setEditItem(product.id);
  };

  const handleDelete = (id) => {
    if (window.confirm("Supprimer ce produit ?")) {
      setProducts(products.filter(p => p.id !== id));
    }
  };

  return (
    <div className="min-h-screen bg-slate-50 p-6">
      <div className="max-w-6xl mx-auto">
        <header className="mb-8 flex items-center justify-between">
          <h1 className="text-3xl font-bold">Catalogue d'affiliation</h1>
          <button
            onClick={() => setAdminMode(!adminMode)}
            className="px-4 py-2 bg-orange-600 text-white rounded-lg shadow hover:bg-orange-700"
          >
            {adminMode ? "Quitter admin" : "Admin"}
          </button>
        </header>

        {adminMode && (
          <div className="mb-10 bg-white p-6 rounded-xl shadow">
            <h2 className="text-xl font-semibold mb-4">{editItem ? "Modifier un produit" : "Ajouter un produit"}</h2>

            <form className="grid grid-cols-1 md:grid-cols-2 gap-4" onSubmit={handleSubmit}>
              <input
                className="p-3 border rounded-lg"
                placeholder="Nom du produit"
                value={form.title}
                onChange={(e) => setForm({ ...form, title: e.target.value })}
                required
              />
              <input
                className="p-3 border rounded-lg"
                placeholder="Prix"
                value={form.price}
                onChange={(e) => setForm({ ...form, price: e.target.value })}
                required
              />
              <input
                className="p-3 border rounded-lg col-span-1 md:col-span-2"
                placeholder="Image (URL)"
                value={form.image}
                onChange={(e) => setForm({ ...form, image: e.target.value })}
                required
              />
              <textarea
                className="p-3 border rounded-lg col-span-1 md:col-span-2"
                placeholder="Description"
                value={form.description}
                onChange={(e) => setForm({ ...form, description: e.target.value })}
                required
              />
              <input
                className="p-3 border rounded-lg col-span-1 md:col-span-2"
                placeholder="Lien d'affiliation"
                value={form.affiliate_url}
                onChange={(e) => setForm({ ...form, affiliate_url: e.target.value })}
                required
              />

              <button type="submit" className="px-4 py-2 bg-indigo-600 text-white rounded-lg shadow col-span-1 md:col-span-2">
                {editItem ? "Enregistrer les modifications" : "Ajouter"}
              </button>
            </form>
          </div>
        )}

        <div className="mb-6">
          <input
            placeholder="Rechercher un produit..."
            value={query}
            onChange={(e) => setQuery(e.target.value)}
            className="w-full p-3 border rounded-lg shadow-sm"
          />
        </div>

        <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
          {filtered.map(product => (
            <div key={product.id} className="bg-white rounded-xl p-4 shadow flex flex-col">
              <img src={product.image} alt={product.title} className="rounded-lg h-40 w-full object-cover" />
              <h3 className="text-lg font-semibold mt-3">{product.title}</h3>
              <p className="text-slate-600 text-sm mt-2 line-clamp-2">{product.description}</p>
              <div className="flex items-center justify-between mt-4">
                <span className="text-xl font-bold">{product.price}</span>
                <button
                  onClick={() => setSelected(product)}
                  className="px-3 py-1 bg-slate-200 rounded-md"
                >Détails</button>
              </div>

              {adminMode && (
                <div className="flex gap-2 mt-3">
                  <button
                    onClick={() => handleEdit(product)}
                    className="flex-1 py-1 bg-blue-600 text-white rounded-md"
                  >Modifier</button>
                  <button
                    onClick={() => handleDelete(product.id)}
                    className="flex-1 py-1 bg-red-600 text-white rounded-md"
                  >Supprimer</button>
                </div>
              )}
            </div>
          ))}
        </div>

        {selected && (
          <div className="fixed inset-0 bg-black/50 flex items-center justify-center z-50">
            <div className="bg-white rounded-xl p-6 max-w-lg w-full shadow-lg">
              <img src={selected.image} alt="" className="rounded-lg w-full h-48 object-cover" />
              <h3 className="text-2xl font-bold mt-4">{selected.title}</h3>
              <p className="text-gray-700 mt-4">{selected.description}</p>
              <div className="flex justify-between items-center mt-6">
                <span className="text-xl font-semibold">{selected.price}</span>
                <a
                  href={selected.affiliate_url}
                  target="_blank"
                  className="px-4 py-2 bg-emerald-600 text-white rounded-lg"
                >Acheter</a>
              </div>
              <button
                onClick={() => setSelected(null)}
                className="w-full mt-5 py-2 border rounded-lg"
              >Fermer</button>
            </div>
          </div>
        )}
      </div>
    </div>
  );
}
