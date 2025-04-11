<script setup>
import { ref, reactive, computed } from 'vue';


const slike = {
    "Jabuka": "https://www.svgrepo.com/show/530203/apple.svg",
    "Mrkva": "https://www.svgrepo.com/show/530216/carrot.svg",
    "Sir": "https://www.svgrepo.com/show/530219/cake.svg",
    "Kruh": "https://www.svgrepo.com/show/530223/bread.svg",
};

const proizvodi = reactive([
    { naziv: "Jabuka", cijena: 0.25 },
    { naziv: "Mrkva", cijena: 0.12 },
    { naziv: "Kruh", cijena: 2.00 },
    { naziv: "Sir", cijena: 4.48 }
]);

const korisnik = reactive({
    jeAdmin: true,
    osobni_podaci: {
        ime: "Marko",
        prezime: "Krivić",
        adresa: {
            grad: "Pula",
            ulica: "Veruda",
            broj: 32
        },
        broj_telefona: "+091-123-456"
    },
    kosarica: reactive([
        { naziv: "Jabuka", količina: 4 },
        { naziv: "Mrkva", količina: 12 },
        { naziv: "Sir", količina: 1 },
        { naziv: "Kruh", količina: 3 },
    ])
});


const isAdmin = ref(true)
const isNotAdmin = ref(false)

const checkAdmin = () => ({
    'text-blue-600': isAdmin.value,
    'text-black': isNotAdmin.value
})

const dohvatiCijenu = (naziv) => {
    const proizvod = proizvodi.find(p => p.naziv === naziv);
    return proizvod ? proizvod.cijena : 0;
}

const sveukupnaCijena = (naziv) => {
    if (naziv == "Jabuka") {
        return proizvodi[0].cijena * korisnik.kosarica[0].količina
    }
    if (naziv == "Mrkva") {
        return proizvodi[1].cijena * korisnik.kosarica[1].količina
    }
    if (naziv == "Kruh") {
        return proizvodi[2].cijena * korisnik.kosarica[3].količina
    }
    if (naziv == "Sir") {
        return proizvodi[3].cijena * korisnik.kosarica[2].količina
    }
}

</script>

<template>
    <div class=" border border-gray-600 rounded-lg  mb-4 w-[300px]">
        <p :class="checkAdmin()">
            <b>Korisnički podaci:</b>
            <br>
            Ime: {{ korisnik.osobni_podaci.ime }}
            <br>
            Prezime: {{ korisnik.osobni_podaci.prezime }}
            <br>
            Adresa: {{ korisnik.osobni_podaci.adresa.ulica }} {{ korisnik.osobni_podaci.adresa.broj }},{{
                korisnik.osobni_podaci.adresa.grad }}
            <br>
            Broj telefona: {{ korisnik.osobni_podaci.broj_telefona }}
        </p>
    </div>
    <br>
    <div
        class=" border border-gray-600 rounded-lg w-[300px] p-4 mb-6 flex flex-col items-center justify-center min-h-screen bg-gray-100">

        <ol>
            <!-- Jabuka -->

            <li class=" border border-gray-600 rounded-lg my-4 w-[300px] flex items-center">
                <p><b>{{ korisnik.kosarica[0].naziv }}</b>
                    <br>
                    <img :src="slike[korisnik.kosarica[0].naziv]" alt="slika" class="w-12 h-12" />
                    cijena: €{{ dohvatiCijenu(korisnik.kosarica[0].naziv) }}
                    <br>
                    količina: {{ korisnik.kosarica[0].količina }}
                    <br>
                    ukupno: €{{ sveukupnaCijena("Jabuka") }}
                </p>
            </li>

            <br>
            <!-- Mrkva -->

            <li class=" border border-gray-600 rounded-lg my-4 w-[300px] flex items-center">
                <p><b>{{ korisnik.kosarica[1].naziv }}</b>
                    <br>
                    <img :src="slike[korisnik.kosarica[1].naziv]" alt="slika" class="w-12 h-12" />
                    cijena: €{{ dohvatiCijenu(korisnik.kosarica[1].naziv) }}
                    <br>
                    količina: {{ korisnik.kosarica[1].količina }}
                    <br>
                    ukupno: €{{ sveukupnaCijena("Mrkva") }}
                </p>
            </li>
            <br>
            <!-- Kruh -->
            <li class=" border border-gray-600 rounded-lg my-4 w-[300px] flex items-center">
                <p><b>{{ korisnik.kosarica[3].naziv }}</b>
                    <br>
                    <img :src="slike[korisnik.kosarica[3].naziv]" alt="slika" class="w-12 h-12" />
                    cijena: €{{ dohvatiCijenu(korisnik.kosarica[3].naziv) }}
                    <br>
                    količina: {{ korisnik.kosarica[3].količina }}
                    <br>
                    ukupno: €{{ sveukupnaCijena("Kruh") }}
                </p>
            </li>
            <br>
            <!--Sir-->
            <li class=" border border-gray-600 rounded-lg my-4 w-[300px] flex items-center">
                <p><b>{{ korisnik.kosarica[2].naziv }}</b>
                    <br>
                    <img :src="slike[korisnik.kosarica[2].naziv]" alt="slika" class="w-12 h-12" />
                    cijena: €{{ dohvatiCijenu(korisnik.kosarica[2].naziv) }}
                    <br>
                    količina: {{ korisnik.kosarica[2].količina }}
                    <br>
                    ukupno: €{{ sveukupnaCijena("Sir") }}
                </p>
            </li>
        </ol>
    </div>
</template>

<style scoped></style>
