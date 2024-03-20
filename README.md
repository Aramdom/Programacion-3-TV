package programaciónIII;
import java.awt.event.FocusEvent;
import java.awt.event.FocusListener;
import javax.swing.JFrame;
import javax.swing.SwingUtilities;

public class Main {

	public static void main(String[] args) {
	    SwingUtilities.invokeLater(new Runnable() {
	        @Override
	        public void run() {
	            new Display();
	        }
	    });

	}
}

//clase display
package programaciónIII;

import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.util.ArrayList;
import java.util.List;
import java.util.Random;

public class Display extends JFrame {
    JPanel panel;
    List<JButton> botonesGenerados;

    public Display() {
        setTitle("Generador de Botones Aleatorios");
        setSize(400, 400);
        setLocationRelativeTo(null);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        panel = new JPanel();
        panel.setLayout(null);
        getContentPane().add(panel);

        JLabel label = new JLabel("Click aquí");
        label.setBounds(150, 150, 100, 30);
        label.addMouseListener(new MouseAdapter() {
            @Override
            public void mouseClicked(MouseEvent e) {
                super.mouseClicked(e);
                generarBotonAleatorio();
            }
        });
        panel.add(label);

        JButton btnLimpiar = new JButton("Limpiar pantalla");
        btnLimpiar.setBounds(120, 200, 160, 30);
        btnLimpiar.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                limpiarPantalla();
            }
        });
        panel.add(btnLimpiar);

        botonesGenerados = new ArrayList<>();

        setVisible(true);
    }

    private void generarBotonAleatorio() {
        Random rand = new Random();
        JButton boton = new JButton("Botón");
        int x = rand.nextInt(panel.getWidth() - boton.getWidth());
        int y = rand.nextInt(panel.getHeight() - boton.getHeight());
        boton.setBounds(x, y, 80, 30);
        boton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                mostrarCoordenadas(boton.getX(), boton.getY());
            }
        });
        botonesGenerados.add(boton);
        panel.add(boton);
        panel.repaint();
    }

    private void limpiarPantalla() {
        for (JButton boton : botonesGenerados) {
            panel.remove(boton);
        }
        botonesGenerados.clear();
        panel.repaint();
    }

    private void mostrarCoordenadas(int x, int y) {
        JOptionPane.showMessageDialog(panel, "Coordenadas del botón: (" + x + ", " + y + ")");
    }

    public static void main(String[] args) {
        new Display();
    }
}


