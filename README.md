/* Додано навігаційне меню для перемикання між сторінками сайту. */

// ==== 1. Навігаційний компонент ==== // // Файл: components/Navbar.tsx

'use client'; import Link from 'next/link'; import { useEffect, useState } from 'react'; import { usePathname } from 'next/navigation'; import LogoutButton from './LogoutButton';

export default function Navbar() { const [isLoggedIn, setIsLoggedIn] = useState(false); const pathname = usePathname();

useEffect(() => { setIsLoggedIn(!!localStorage.getItem('token')); }, [pathname]);

return ( <nav className="bg-gray-900 text-white p-4 flex justify-between items-center"> <div className="flex gap-4"> <Link href="/" className="hover:underline">Головна</Link> {isLoggedIn && <Link href="/history" className="hover:underline">Історія ставок</Link>} </div> <div className="flex gap-4"> {!isLoggedIn ? ( <> <Link href="/login" className="hover:underline">Вхід</Link> <Link href="/register" className="hover:underline">Реєстрація</Link> </> ) : ( <LogoutButton /> )} </div> </nav> ); }

// ==== 2. Вставити Navbar у layout.tsx ==== // // Файл: app/layout.tsx

// ... // import Navbar from '@/components/Navbar'; // ... // <body> //   <Navbar /> //   {children} // </body>

