# Pc-Smith-Store
import React, { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { ShoppingCart } from "lucide-react";
import { Carousel } from "@/components/ui/carousel";

// Sample products and gallery images
const products = [
  { id: 1, name: "PCSmith Elite Gaming Rig", price: "₹1,50,000", image: "https://example.com/elite-gaming-rig.jpg" },
  { id: 2, name: "PCSmith Workstation Pro", price: "₹2,00,000", image: "https://example.com/workstation-pro.jpg" },
  { id: 3, name: "PCSmith Budget Beast", price: "₹80,000", image: "https://example.com/budget-beast.jpg" },
  { id: 4, name: "PCSmith Ultra Gaming Beast", price: "₹2,50,000", image: "https://example.com/ultra-gaming-beast.jpg" },
  { id: 5, name: "PCSmith Mini Workstation", price: "₹1,20,000", image: "https://example.com/mini-workstation.jpg" },
  { id: 6, name: "PCSmith Extreme Overkill", price: "₹3,00,000", image: "https://example.com/extreme-overkill.jpg" },
  { id: 7, name: "PCSmith Ultimate Creator", price: "₹1,80,000", image: "https://example.com/ultimate-creator.jpg" },
  { id: 8, name: "PCSmith Streamer Pro", price: "₹2,20,000", image: "https://example.com/streamer-pro.jpg" }
];

const galleryImages = [
  "https://example.com/gallery1.jpg",
  "https://example.com/gallery2.jpg",
  "https://example.com/gallery3.jpg",
  "https://example.com/gallery4.jpg",
  "https://example.com/gallery5.jpg"
];

export default function Store() {
  const [activeTab, setActiveTab] = useState("home");
  const [cart, setCart] = useState([]);

  // Add item to cart
  const addToCart = (product) => {
    setCart([...cart, product]);
  };

  // Remove item from cart
  const removeFromCart = (id) => {
    setCart(cart.filter(item => item.id !== id));
  };

  return (
    <div className="bg-gradient-to-br from-black via-gray-900 to-black text-white min-h-screen font-sans transition-all ease-in-out duration-500">
      <nav className="flex justify-between px-8 py-6 text-lg font-medium bg-gray-800 shadow-md fixed top-0 w-full z-50 backdrop-blur-md">
        <div className="flex space-x-8">
          {["Home", "Gallery", "Products", "Contact", "About"].map((name, index) => (
            <button
              key={index}
              onClick={() => setActiveTab(name.toLowerCase())}
              className={`px-4 py-2 rounded-lg transition-all duration-300 ${activeTab === name.toLowerCase() ? "bg-[#C8963E] text-black shadow-lg" : "text-gray-400 hover:text-[#C8963E]"}`}
            >
              {name}
            </button>
          ))}
        </div>
        <button onClick={() => setActiveTab("cart")} className="relative">
          <ShoppingCart className="w-8 h-8 text-white hover:text-[#C8963E]" />
          {cart.length > 0 && (
            <span className="absolute top-0 right-0 bg-red-600 text-white text-xs rounded-full px-2 py-1">{cart.length}</span>
          )}
        </button>
      </nav>

      <div className="flex justify-center mt-24">
        <img src="https://i.imgur.com/HpRRreR.png" alt="PCSmith Logo" className="h-20" />
      </div>

      <div className="p-8 max-w-6xl mx-auto mt-8">
        {/* Home Tab */}
        {activeTab === "home" && (
          <div className="text-center">
            <h1 className="text-5xl font-extrabold text-[#C8963E]">PCSmith Custom Builds</h1>
            <p className="text-lg text-gray-400 mt-4">High-performance, custom-built PCs tailored for your needs.</p>
            <div className="mt-8 flex justify-center">
              <Button onClick={() => setActiveTab("products")} className="bg-[#C8963E] hover:bg-[#B07D35] text-black text-lg font-semibold px-6 py-3 rounded-xl transition-all duration-300 shadow-lg">Explore Builds</Button>
            </div>
            <div className="mt-12">
              <Carousel>
                {galleryImages.map((src, index) => (
                  <img key={index} src={src} alt={`Showcase ${index + 1}`} className="rounded-xl shadow-md" />
                ))}
              </Carousel>
            </div>
          </div>
        )}

        {/* Products Tab */}
        {activeTab === "products" && (
          <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8">
            {products.map((product) => (
              <Card key={product.id} className="bg-gray-800 rounded-xl shadow-lg">
                <img src={product.image} alt={product.name} className="rounded-t-xl w-full h-64 object-cover" />
                <CardContent className="text-center p-4">
                  <h2 className="text-xl font-semibold text-[#C8963E]">{product.name}</h2>
                  <p className="text-lg text-gray-400 mt-2">{product.price}</p>
                  <Button
                    onClick={() => addToCart(product)}
                    className="mt-4 bg-[#C8963E] hover:bg-[#B07D35] text-black font-semibold px-6 py-3 rounded-xl transition-all duration-300"
                  >
                    Add to Cart
                  </Button>
                </CardContent>
              </Card>
            ))}
          </div>
        )}

        {/* Cart Tab */}
        {activeTab === "cart" && (
          <div className="text-center text-lg text-gray-300 mt-12">
            <h2 className="text-3xl font-bold text-[#C8963E]">Your Cart</h2>
            {cart.length === 0 ? (
              <p>Your cart is empty.</p>
            ) : (
              <ul className="mt-4">
                {cart.map((item, index) => (
                  <li key={index} className="mt-2 flex justify-between">
                    <span>{item.name} - {item.price}</span>
                    <button
                      onClick={() => removeFromCart(item.id)}
                      className="text-red-600 hover:text-red-500"
                    >
                      Remove
                    </button>
                  </li>
                ))}
              </ul>
            )}
          </div>
        )}
      </div>
    </div>
  );
}
