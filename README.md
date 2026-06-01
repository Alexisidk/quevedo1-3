import time
import random

class Protagonista:
    def __init__(self, nombre, habilidad, arma_corta):
        self.nombre = nombre
        self.habilidad = habilidad
        self.arma_corta = arma_corta
        self.armas_largas = []  # Máximo 2 por realismo
        self.dinero_sucio = 0
        self.dinero_limpio = 0

    def equipar_arma_larga(self, arma):
        if len(self.armas_largas) < 2:
            self.armas_largas.append(arma)
            print(f"[{self.nombre}] Equipó {arma} en la espalda.")
        else:
            print(f"❌ [{self.nombre}] ¡No puedes llevar más de 2 armas largas! Usa el maletero.")

    def usar_habilidad(self):
        print(f"\n🔥 [HABILIDAD] {self.nombre} activó: {self.habilidad}!")
        time.sleep(1)


class VehiculoMision:
    def __init__(self, modelo):
        self.modelo = modelo
        self.maletero = []
        self.nivel_busqueda = 0

    def guardar_en_maletero(self, item):
        self.maletero.append(item)
        print(f"📦 Guardado '{item}' en el maletero del {self.modelo}.")


class SistemaGta6:
    def __init__(self):
        self.lucia = Protagonista("Lucia", "Hacker de Seguridad (Cámaras OFF)", "Pistola 9mm")
        self.jason = Protagonista("Jason", "Reflejos de Conducción (Bullet Time)", "Revólver .38")
        self.personaje_actual = self.lucia
        self.coche = VehiculoMision("Bravado Banshee TT")

    def cambiar_personaje(self):
        # Simulación de zoom satelital sin pantallas de carga
        print("\n--- INICIANDO CAMBIO DE PERSONAJE (ZOOM SATELITAL) ---")
        print("🛸 Alejando cámara al espacio...")
        time.sleep(0.5)
        print("📍 Enfocando nueva ubicación en Vice City...")
        time.sleep(0.5)
        
        if self.personaje_actual == self.lucia:
            self.personaje_actual = self.jason
        else:
            self.personaje_actual = self.lucia
            
        print(f"✅ Controlando ahora a: {self.personaje_actual.nombre}")
        print("-------------------------------------------------------\n")

    def iniciar_atraco(self):
        print(f"--- COMENZANDO ATRACO EN PORT GELLHORN con {self.personaje_actual.nombre} ---")
        
        # 1. Uso de habilidades según el personaje actual
        self.personaje_actual.usar_habilidad()
        
        # 2. Mecánica de botín y policía
        botin = random.randint(5000, 25000)
        self.personaje_actual.dinero_sucio += botin
        self.coche.nivel_busqueda = 3
        print(f"💰 ¡Robo exitoso! Botín: ${botin} (Dinero Sucio).")
        print(f"🚨 Alerta: Nivel de búsqueda actual: {'⭐' * self.coche.nivel_busqueda}")
        
        # 3. Escape inteligente (Evita spawn aleatorio de policía)
        print("\n🚓 La policía está patrullando las calles usando cámaras de tráfico...")
        time.sleep(1)
        print("🏎️  ¡Lograste perderlos en los callejones de Vice City Beach!")
        self.coche.nivel_busqueda = 0
        print("✅ Nivel de búsqueda: Limpio.")

    def estado_partida(self):
        print("\n================ ESTADO DE LA PARTIDA ================")
        print(f"🕹️  Personaje Activo: {self.personaje_actual.nombre}")
        print(f"💵 Dinero Sucio: ${self.personaje_actual.dinero_sucio} | Dinero Limpio: ${self.personaje_actual.dinero_limpio}")
        print(f"🎒 Armas encima: [{self.personaje_actual.arma_corta}] + {self.personaje_actual.armas_largas}")
        print(f"🚗 Maletero del {self.coche.modelo}: {self.coche.maletero}")
        print("======================================================\n")


# --- SIMULACIÓN DEL JUEGO EN EJECUCIÓN ---
if __name__ == "__main__":
    juego = SistemaGta6()
    
    # 1. Configuración inicial de inventario (Sin "bolsillos mágicos")
    juego.lucia.equipar_arma_larga("Fusil de Asalto Carbina")
    juego.lucia.equipar_arma_larga("Escopeta Recortada")
    juego.lucia.equipar_arma_larga("Lanzacohetes") # Esto fallará por espacio
    
    # Guardamos el exceso en el coche
    juego.coche.guardar_en_maletero("Lanzacohetes")
    juego.coche.guardar_en_maletero("Sniper Pesado")
    
    juego.estado_partida()

    # 2. Ejecutar un atraco con Lucia
    juego.iniciar_atraco()
    juego.estado_partida()

    # 3. Cambiar a Jason de forma fluida para usar su vehículo
    juego.cambiar_personaje()
    
    # 4. Jason realiza otra acción
    juego.iniciar_atraco()
    juego.estado_partida()
