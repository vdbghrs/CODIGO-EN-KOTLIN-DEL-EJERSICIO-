# CODIGO-EN-KOTLIN-DEL-EJERSICIO-

import java.util.Locale

fun leerMonto(): Double {

    while (true) {

        print("Ingrese el monto total T: ")

        val entrada = readLine()?.trim()?.replace(",", ".")

        val monto = entrada?.toDoubleOrNull()

        if (monto != null && monto.isFinite() && monto >= 0) {
            return monto
        }

        println("ERROR: Ingrese un monto numerico valido.")
        println("Ejemplo: 5000 o 5000.50")
        println()
    }
}

fun calcularRemesa(T: Double): Double {

    val itf = 0.00005

    // Caso 1: mr <= 1000
    val mr1 = (T - 5.0) / (1.0 + itf)

    if (mr1 >= 0.0 && mr1 <= 1000.0) {
        return mr1
    }

    // Caso 2: 1000 < mr <= 10001
    val mr2 = T / (1.0 + 0.005 + itf)

    if (mr2 > 1000.0 && mr2 <= 10001.0) {
        return mr2
    }

    // Caso 3: mr > 10001
    val mr3 = T / (1.0 + 0.015 + itf)

    return mr3
}

fun calcularComision(mr: Double): Double {

    return when {
        mr <= 1000.0 -> 5.0
        mr <= 10001.0 -> mr * 0.005
        else -> mr * 0.015
    }
}

fun calcularITF(mr: Double): Double {

    return mr * 0.00005
}

fun main() {

    Locale.setDefault(Locale.US)

    println("====================================")
    println("       CALCULO DE REMESA")
    println("====================================")

    val T = leerMonto()

    // El menor monto posible considerando una remesa de 0
    if (T < 5.0) {

        println()
        println("====================================")
        println("No existe una remesa valida para")
        println("el monto total ingresado.")
        println("El monto total minimo es 5.00")
        println("====================================")

        return
    }

    val mr = calcularRemesa(T)
    val comision = calcularComision(mr)
    val itf = calcularITF(mr)

    println()
    println("====================================")
    println("            RESULTADOS")
    println("====================================")
    println("Monto total T : %.2f".format(T))
    println("Monto remesa  : %.2f".format(mr))
    println("Comision      : %.2f".format(comision))
    println("ITF           : %.2f".format(itf))
    println("====================================")

    println()
    println("Verificacion:")
    println("mr + comision + ITF = %.2f".format(mr + comision + itf))
}
