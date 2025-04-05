import sqlite3

# Conectar a la base de datos (o crearla si no existe)
conn = sqlite3.connect('telefonos.db')
cursor = conn.cursor()

# Crear la tabla para almacenar los números telefónicos
cursor.execute('''
CREATE TABLE IF NOT EXISTS telefonos (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nombre TEXT,
    telefono TEXT
)
''')

# Insertar algunos números de teléfono en la tabla
telefonos = [
    ('Juan Pérez', '555-1234'),
    ('Ana Gómez', '555-5678'),
    ('Carlos López', '555-9876'),
    ('Marta Rodríguez', '555-4321')
]

cursor.executemany('''
INSERT INTO telefonos (nombre, telefono)
VALUES (?, ?)
''', telefonos)

# Confirmar los cambios
conn.commit()

# Consultar los números de teléfono en la base de datos
cursor.execute('SELECT * FROM telefonos')
resultados = cursor.fetchall()

# Mostrar los resultados
for fila in resultados:
    print(f"ID: {fila[0]}, Nombre: {fila[1]}, Teléfono: {fila[2]}")

# Cerrar la conexión
conn.close()
