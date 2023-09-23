# parcial-2

import java.util.ArrayList;

import java.util.List;

// Interfaz para definir el comportamiento de un boleto
interface Boleto {
    void mostrarInformacion();
}

// Implementación concreta de un boleto para una atracción específica
class BoletoAtraccion implements Boleto {
    private String nombreAtraccion;
    private double precio;

    public BoletoAtraccion(String nombreAtraccion, double precio) {
        this.nombreAtraccion = nombreAtraccion;
        this.precio = precio;
    }

    @Override
    public void mostrarInformacion() {
        System.out.println("Boleto para la atracción: " + nombreAtraccion);
        System.out.println("Precio: $" + precio);
    }
}

// Interfaz para definir el comportamiento de una atracción
interface Atraccion {
    void operar();
}

// Implementación concreta de una atracción
class MontañaRusa implements Atraccion {
    private String nombre;

    public MontañaRusa(String nombre) {
        this.nombre = nombre;
    }

    @Override
    public void operar() {
        System.out.println("Operando la Montaña Rusa: " + nombre);
        // Lógica de funcionamiento de la atracción
    }
}

// Fabrica abstracta para crear boletos
abstract class FabricaBoletos {
    public abstract Boleto crearBoleto();
}

// Fabrica concreta para crear boletos de atracciones
class FabricaBoletosAtraccion extends FabricaBoletos {
    private String nombreAtraccion;
    private double precio;

    public FabricaBoletosAtraccion(String nombreAtraccion, double precio) {
        this.nombreAtraccion = nombreAtraccion;
        this.precio = precio;
    }

    @Override
    public Boleto crearBoleto() {
        return new BoletoAtraccion(nombreAtraccion, precio);
    }
}

public class ParqueDeDiversiones {
    public static void main(String[] args) {
        List<Atraccion> atracciones = new ArrayList<>();
        atracciones.add(new MontañaRusa("Montaña Rusa 1"));
        atracciones.add(new MontañaRusa("Montaña Rusa 2"));

        List<Boleto> boletos = new ArrayList<>();
        FabricaBoletos fabricaBoletos = new FabricaBoletosAtraccion("Montaña Rusa 1", 10.0);
        boletos.add(fabricaBoletos.crearBoleto());
        fabricaBoletos = new FabricaBoletosAtraccion("Montaña Rusa 2", 12.0);
        boletos.add(fabricaBoletos.crearBoleto());

        // Operar atracciones
        for (Atraccion atraccion : atracciones) {
            atraccion.operar();
        }

        // Mostrar información de boletos
        for (Boleto boleto : boletos) {
            boleto.mostrarInformacion();
        }
    }
}
