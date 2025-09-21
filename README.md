import React, { useState } from "react";

// AI-Marketplace-Assistant-Prototype.jsx // Single-file React component prototype (Tailwind CSS assumed available) // Default export: PrototypeApp

export default function PrototypeApp() { const [screen, setScreen] = useState("home"); const [artisanName, setArtisanName] = useState("Shanti Handlooms"); const [products, setProducts] = useState([ { id: 1, title: "Block-printed Scarf", price: 850, img: null, story: "Hand-block printed by artisan Shanti in Rajasthan.", }, { id: 2, title: "Terracotta Tea Light", price: 350, img: null, story: "Locally fired terracotta, crafted in clay-rich soil.", }, ]);

const [newProduct, setNewProduct] = useState({ title: "", price: "", story: "" }); const [chat, setChat] = useState([ { id: 1, who: "assistant", text: "Hi! I can help list a product or suggest pricing." }, ]); const [message, setMessage] = useState("");

function addProduct() { if (!newProduct.title) return; const p = { id: Date.now(), title: newProduct.title, price: Number(newProduct.price) || 0, story: newProduct.story || "", }; setProducts([p, ...products]); setNewProduct({ title: "", price: "", story: "" }); setScreen("catalog"); }

function aiSuggestPrice(title) { // Mock AI suggestion: base on title length + randomness const base = Math.max(100, title.length * 25); const suggested = Math.round(base * (1 + (Math.random() - 0.4) * 0.25)); return suggested; }

function handleAskAI() { if (!message.trim()) return; // Mock response: echo + suggestion const suggestion = aiSuggestPrice(message); const resp = Nice product idea. Suggested price: ₹${suggestion}. I can auto-generate a listing for you.; setChat([...chat, { id: Date.now(), who: "user", text: message }, { id: Date.now() + 1, who: "assistant", text: resp }]); setMessage(""); }

// Simple components const Header = () => ( <header className="flex items-center justify-between p-4 bg-white shadow-sm rounded-b-lg"> <div className="flex items-center gap-3"> <div className="w-12 h-12 rounded-lg bg-gradient-to-br from-indigo-500 to-pink-500 flex items-center justify-center text-white font-bold">AI</div> <div> <div className="text-sm text-gray-500">AI Marketplace Assistant</div> <div className="font-semibold">{artisanName}</div> </div> </div> <nav className="flex gap-3"> <button onClick={() => setScreen("home")} className={px-3 py-2 rounded ${screen==="home"?"bg-gray-100":"hover:bg-gray-50"}}> Home </button> <button onClick={() => setScreen("catalog")} className={px-3 py-2 rounded ${screen==="catalog"?"bg-gray-100":"hover:bg-gray-50"}}> Catalog </button> <button onClick={() => setScreen("add")} className={px-3 py-2 rounded ${screen==="add"?"bg-gray-100":"hover:bg-gray-50"}}> Add Product </button> <button onClick={() => setScreen("assist")} className={px-3 py-2 rounded ${screen==="assist"?"bg-gray-100":"hover:bg-gray-50"}}> AI Assistant </button> </nav> </header> );

const Home = () => ( <div className="p-6 grid grid-cols-1 md:grid-cols-3 gap-6"> <div className="col-span-2 bg-white p-6 rounded-lg shadow"> <h2 className="text-xl font-semibold mb-2">Welcome, {artisanName}</h2> <p className="text-gray-600">Your AI assistant helps you create listings, suggest prices, write product stories, and draft social posts.</p>

<div className="mt-6 grid grid-cols-1 sm:grid-cols-2 gap-4">
      <div className="p-4 bg-gray-50 rounded">
        <h3 className="font-semibold">Quick Actions</h3>
        <ul className="mt-2 text-sm text-gray-700">
          <li>• Suggest price for a new product</li>
          <li>• Auto-generate product description</li>
          <li>• Create shareable social post</li>
        </ul>
        <div className="mt-4 flex gap-2">
          <button onClick={() => setScreen("assist")} className="px-3 py-2 rounded bg-indigo-600 text-white">Open Assistant</button>
          <button onClick={() => setScreen("add")} className="px-3 py-2 rounded border">Add Product</button>
        </div>
      </div>

      <div className="p-4 bg-gray-50 rounded">
        <h3 className="font-semibold">Sales Snapshot</h3>
        <div className="mt-2 text-2xl font-bold">₹{products.reduce((s,p)=>s+p.price,0)}</div>
        <div className="text-sm text-gray-500">Total (mock) value of listed products</div>
      </div>
    </div>
  </div>

  <aside className="bg-white p-4 rounded-lg shadow">
    <h3 className="font-semibold mb-2">Featured Product</h3>
    {products[0] ? (
      <div>
        <div className="text-lg font-semibold">{products[0].title}</div>
        <div className="text-sm text-gray-500">₹{products[0].price}</div>
        <p className="mt-2 text-gray-600">{products[0].story}</p>
        <div className="mt-3 flex gap-2">
          <button className="px-3 py-2 rounded border">Share</button>
          <button className="px-3 py-2 rounded bg-emerald-500 text-white">Promote</button>
        </div>
      </div>
    ) : (
      <div className="text-gray-500">No products yet.</div>
    )}
  </aside>
</div>

);

const Catalog = () => ( <div className="p-6"> <h2 className="text-xl font-semibold mb-4">Catalog</h2> <div className="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4"> {products.map((p) => ( <div key={p.id} className="bg-white rounded-lg p-4 shadow"> <div className="h-36 bg-gray-100 rounded flex items-center justify-center">Image</div> <div className="mt-3"> <div className="font-semibold">{p.title}</div> <div className="text-sm text-gray-500">₹{p.price}</div> <p className="text-gray-600 mt-2 text-sm">{p.story}</p> </div> <div className="mt-3 flex gap-2"> <button className="px-2 py-1 rounded border text-sm">Edit</button> <button className="px-2 py-1 rounded border text-sm">Share</button> </div> </div> ))} </div> </div> );

const AddProduct = () => ( <div className="p-6"> <h2 className="text-xl font-semibold mb-4">Add Product</h2> <div className="bg-white p-6 rounded shadow max-w-2xl"> <label className="block mb-2 text-sm">Title</label> <input value={newProduct.title} onChange={(e)=>setNewProduct({...newProduct, title: e.target.value})} className="w-full border p-2 rounded mb-3" placeholder="E.g., Handwoven Shawl" />

<label className="block mb-2 text-sm">Suggested Price (₹)</label>
    <div className="flex gap-2 mb-3">
      <input value={newProduct.price} onChange={(e)=>setNewProduct({...newProduct, price: e.target.value})} className="flex-1 border p-2 rounded" placeholder="e.g. 1200" />
      <button onClick={()=>setNewProduct({...newProduct, price: aiSuggestPrice(newProduct.title || 'product')})} className="px-3 py-2 rounded bg-gray-100">AI Suggest</button>
    </div>

    <label className="block mb-2 text-sm">Story / Description</label>
    <textarea value={newProduct.story} onChange={(e)=>setNewProduct({...newProduct, story: e.target.value})} className="w-full border p-2 rounded mb-3" rows={4} placeholder="Tell the story behind this product"></textarea>

    <div className="flex gap-2">
      <button onClick={addProduct} className="px-4 py-2 rounded bg-indigo-600 text-white">Create Listing</button>
      <button onClick={()=>{setNewProduct({title:'',price:'',story:''})}} className="px-4 py-2 rounded border">Reset</button>
    </div>
  </div>
</div>

);

const Assistant = () => ( <div className="p-6 grid grid-cols-1 md:grid-cols-3 gap-6"> <div className="md:col-span-2 bg-white p-4 rounded shadow"> <h2 className="text-lg font-semibold mb-3">AI Assistant</h2> <div className="h-96 overflow-auto p-3 bg-gray-50 rounded"> {chat.map((c)=> ( <div key={c.id} className={mb-3 ${c.who==='assistant'?'text-left':'text-right'}}> <div className={inline-block p-2 rounded ${c.who==='assistant'?'bg-white shadow':'bg-indigo-600 text-white'}}>{c.text}</div> </div> ))} </div>

<div className="mt-3 flex gap-2">
      <input value={message} onChange={(e)=>setMessage(e.target.value)} placeholder="Ask: e.g., suggest price for handloom dupatta" className="flex-1 border p-2 rounded" />
      <button onClick={handleAskAI} className="px-4 py-2 rounded bg-indigo-600 text-white">Send</button>
    </div>

    <div className="mt-3 text-sm text-gray-500">Tip: Type a product name or paste a photo URL. (This prototype mocks AI responses.)</div>
  </div>

  <aside className="bg-white p-4 rounded shadow">
    <h3 className="font-semibold mb-2">Assistant Tools</h3>
    <div className="space-y-3 text-sm">
      <div>
        <div className="font-medium">Auto description</div>
        <div className="text-gray-600">Generate an evocative product description from a few keywords.</div>
      </div>
      <div>
        <div className="font-medium">Social Post</div>
        <div className="text-gray-600">One-click social caption + hashtags optimized for local festivals.</div>
      </div>
      <div>
        <div className="font-medium">Voice input</div>
        <div className="text-gray-600">Artisans can speak their product details (mobile-first).</div>
      </div>
    </div>
  </aside>
</div>

);

return ( <div className="min-h-screen bg-gray-50 p-4"> <div className="max-w-6xl mx-auto"> <Header />

<main className="mt-6 bg-transparent rounded">
      {screen === "home" && <Home />}
      {screen === "catalog" && <Catalog />}
      {screen === "add" && <AddProduct />}
      {screen === "assist" && <Assistant />}
    </main>

    <footer className="mt-8 text-center text-sm text-gray-500">Prototype — AI Marketplace Assistant · Mobile-first · Mock data</footer>
  </div>
</div>

); }

