"use client"

import type React from "react"

import { useState } from "react"
import { useRouter } from "next/navigation"
import { Button } from "@/components/ui/button"
import { Input } from "@/components/ui/input"

export default function LoginPage() {
  const [password, setPassword] = useState("")
  const [error, setError] = useState(false)
  const [showHint, setShowHint] = useState(false)
  const router = useRouter()

  const handleSubmit = (e: React.FormEvent) => {
    e.preventDefault()

    if (password.toLowerCase() === "garammadu") {
      // Store in session storage that user is authenticated
      sessionStorage.setItem("isAuthenticated", "true")
      router.push("/wish")
    } else {
      setError(true)
      if (!showHint) {
        setShowHint(true)
      }
    }
  }

  return (
    <div
      className="min-h-screen flex flex-col items-center justify-center p-4"
      style={{
        background: "linear-gradient(135deg, #e0c3fc 0%, #feb2b2 100%)",
      }}
    >
      <div
        className={`w-full max-w-md p-8 rounded-lg shadow-lg transition-all duration-300 ${
          error ? "bg-red-100" : "bg-white/90"
        }`}
      >
        <h1 className="text-3xl font-bold text-center mb-6 text-purple-800">are you really anna?👀</h1>

        <p className="text-lg text-center mb-8 text-pink-700">if it&apos;s you tulis your fav song</p>

        <form onSubmit={handleSubmit} className="space-y-6">
          <Input
            type="text"
            value={password}
            onChange={(e) => {
              setPassword(e.target.value)
              setError(false)
            }}
            placeholder="Enter the password..."
            className="w-full p-4 border-2 border-purple-300 rounded-md focus:border-pink-500 focus:ring focus:ring-pink-200"
          />

          {showHint && (
            <p className="text-sm italic text-center text-purple-700">Hint: lagu yang sering kita denger di mobil</p>
          )}

          <Button
            type="submit"
            className="w-full py-3 bg-gradient-to-r from-purple-500 to-pink-500 text-white rounded-md hover:from-purple-600 hover:to-pink-600 transition-all"
          >
            Enter
          </Button>
        </form>
      </div>
    </div>
  )
}
