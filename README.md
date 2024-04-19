import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class gui extends JFrame {

    private JPanel panel;
    private JPanel panelInicio;
    private JPanel panelHUD; // Panel para el HUD
    private JLabel nave;
    private JLabel lblPuntuacion;

    private int naveX = 0; // Posición inicial de la nave en el eje X
    private int velocidadNave = 1; // Velocidad de movimiento de la nave
    private int puntuacion = 0;
    private int vidas = 3; // Cantidad inicial de vidas
    
    // Variables para controlar el movimiento continuo de la nave
    private boolean izquierdaPresionada = false;
    private boolean derechaPresionada = false;

    public gui() {
        setTitle("Space Warriors");
        setSize(800, 600); // Tamaño de la ventana
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null); 
        
        panel = new JPanel() {
            @Override
            protected void paintComponent(Graphics g) {
                super.paintComponent(g);
                // Establecer el fondo en blanco y negro
                g.setColor(Color.BLACK);
                g.fillRect(0, 0, getWidth(), getHeight());
            }
        };
       
        panel.setLayout(null);
        
        getContentPane().add(panel);
        
        JButton btnInicio = new JButton();
        btnInicio.setFont(new Font("Tahoma", Font.PLAIN, 11));
        ImageIcon iconoInicio = new ImageIcon("C:/Users/aramd/eclipse-workspace/TRABAJOS1/src/Memorama/IconoDeInicio-removebg-preview.png");
        Image imagenIcono = iconoInicio.getImage().getScaledInstance(100, 100, Image.SCALE_SMOOTH); 
        btnInicio.setIcon(new ImageIcon(imagenIcono));
        btnInicio.setBounds(350, 200, 100, 100);
        panel.add(btnInicio);
        
        JLabel lblTitulo = new JLabel("SPACE WARRIORS");
        lblTitulo.setFont(new Font("Monospaced", Font.BOLD, 44)); 
        lblTitulo.setForeground(new Color(255, 0, 0));
        lblTitulo.setBounds(150, 100, 500, 50);
        panel.add(lblTitulo);
        
        // Crear panel de inicio
        panelInicio = new JPanel() {
            @Override
            protected void paintComponent(Graphics g) {
                super.paintComponent(g);
                // Dibujar la imagen de fondo
                ImageIcon imagenFondoInicio = new ImageIcon("C:/Users/aramd/eclipse-workspace/TRABAJOS1/src/Memorama/Background.jpg");
                g.drawImage(imagenFondoInicio.getImage(), 0, 0, getWidth(), getHeight(), null);
            }
        };
        panelInicio.setLayout(null);
        panelInicio.setBounds(0, 0, 800, 600);
        
        // Crear panel para el HUD
        panelHUD = new JPanel();
        panelHUD.setLayout(new GridLayout(1, 2)); // Diseño de una fila y dos columnas
        panelHUD.setBounds(0, 0, 800, 50); // Posición y tamaño
        panelHUD.setBackground(Color.BLACK); // Color de fondo
        
        // Agregar etiquetas para la puntuación y las vidas al HUD
        JLabel lblEtiquetaPuntuacion = new JLabel("Puntuación: ");
        lblEtiquetaPuntuacion.setForeground(Color.WHITE);
        JLabel lblEtiquetaVidas = new JLabel("Vidas: ");
        lblEtiquetaVidas.setForeground(Color.WHITE);
        
        // Agregar las etiquetas al panel del HUD
        panelHUD.add(lblEtiquetaPuntuacion);
        panelHUD.add(lblEtiquetaVidas);
        
        panelInicio.add(panelHUD);
        
        btnInicio.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                panel.removeAll();
                panel.add(panelInicio);
                
                // Crear la nave
                
                ImageIcon iconoNave = new ImageIcon("C:/Users/aramd/eclipse-workspace/TRABAJOS1/src/Memorama/Nave.gif");
                Image imagenNave = iconoNave.getImage().getScaledInstance(100, 100, Image.SCALE_DEFAULT);
                nave = new JLabel(new ImageIcon(imagenNave));
                nave.setBounds(naveX, 300, 100, 100); // Posición inicial de la nave
                panelInicio.add(nave);

    

                // Agregar KeyListener para mover la nave con las flechas del teclado
                panelInicio.setFocusable(true);
                panelInicio.requestFocusInWindow();
                panelInicio.addKeyListener(new KeyAdapter() {
                    @Override
                    public void keyPressed(KeyEvent e) {
                        int keyCode = e.getKeyCode();
                        if (keyCode == KeyEvent.VK_LEFT) {
                            izquierdaPresionada = true;
                            // Mover la nave directamente aquí
                            naveX -= velocidadNave;
                            nave.setLocation(naveX, 300);
                        } else if (keyCode == KeyEvent.VK_RIGHT) {
                            derechaPresionada = true;
                            // Mover la nave directamente aquí
                            naveX += velocidadNave;
                            nave.setLocation(naveX, 300);
                        } else if (keyCode == KeyEvent.VK_A) {
                            disparar();
                        }
                    }

                    @Override
                    public void keyReleased(KeyEvent e) {
                        int keyCode = e.getKeyCode();
                        if (keyCode == KeyEvent.VK_LEFT) {
                            izquierdaPresionada = false;
                        } else if (keyCode == KeyEvent.VK_RIGHT) {
                            derechaPresionada = false;
                        }
                    }
                });
                
                panel.revalidate();
                panel.repaint();
            }
        });
    }

    private void disparar() {
        // Crear un proyectil en la posición actual de la nave
        Proyectil proyectil = new Proyectil(nave.getX() + nave.getWidth() / 2 - 10, nave.getY());
        
        // Agregar el proyectil al panel donde se encuentra la nave
        panelInicio.add(proyectil);
        
        // Asegurarse de que el proyectil se muestre correctamente
        panelInicio.revalidate();
        panelInicio.repaint();
    }
    
    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            public void run() {
                gui frame = new gui();
                frame.setVisible(true);
            }
        });
    }
}







Message ChatGPT…


ChatGPT can make mistakes. Consider checking important 
