
import java.awt.FlowLayout;
import java.awt.Graphics;
import java.awt.Image;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;
import javax.imageio.ImageIO;
import javax.sound.sampled.AudioInputStream;
import javax.sound.sampled.AudioSystem;
import javax.sound.sampled.Clip;
import javax.swing.JButton;
import javax.swing.JPanel;
import javax.swing.JFrame;

class Panel extends JPanel implements ActionListener,Runnable{
    BufferedImage image;
    JButton bl,br;
    Thread t;
    int x,y,z=500,v=500;
    boolean btf=true,f2=true,f3=true,f4=true;
    boolean f=true;
    Image g1,g2,g3,g4,g5,g6,g7,g8,g9,g10;
    Panel() throws IOException{
        bl = new JButton("Left");
        br = new JButton("Right");
        this.setLayout(new FlowLayout());
        bl.addActionListener(this);
        br.addActionListener(this);
        this.add(bl);
        this.add(br);
        x=-500;
        y=-950;
        this.image = ImageIO.read(new File("C:\\Users\\taksin\\Downloads\\WALK\\BG4.png"));
        g1 = ImageIO.read(new File("C:\\Users\\taksin\\Downloads\\WALK\\WALK1.png"));
        g2 = ImageIO.read(new File("C:\\Users\\taksin\\Downloads\\WALK\\WALK2.png"));
        g3 = ImageIO.read(new File("C:\\Users\\taksin\\Downloads\\WALK\\WALK3.png"));
        g4 = ImageIO.read(new File("C:\\Users\\taksin\\Downloads\\WALK\\WALK4.png"));
        g5 = ImageIO.read(new File("C:\\Users\\taksin\\Downloads\\WALK\\WALK5.png"));
        g6 = ImageIO.read(new File("C:\\Users\\taksin\\Downloads\\WALK\\WALK6.png"));
        g7 = ImageIO.read(new File("C:\\Users\\taksin\\Downloads\\WALK\\WALK7.png"));
        g8 = ImageIO.read(new File("C:\\Users\\taksin\\Downloads\\WALK\\WALK8.png"));
        g9 = ImageIO.read(new File("C:\\Users\\taksin\\Downloads\\WALK\\WALK9.png"));
        
    }
    
    @Override
    public void actionPerformed(ActionEvent e) {
        if("Left".equals(e.getActionCommand())){
            btf=true;
            f2=true;
            f3=true;
           // playSound("C:\\Users\\taksin\\Downloads\\WALK\\CLICK1.mp3");
            start();
        }
        if("Right".equals(e.getActionCommand())){
            btf=false;
            f3=false;
            f4=false;
            start();
        }
    }
    
    public void start(){
        t = new Thread(this);
        t.start();
    }


    @Override
    public void run() {
        Graphics g = this.getGraphics();
        super.paint(g);
        if(btf==true){
        while(true){
             
            if(x>500){
                x=-500;
 	    } 
            else{
                 x+=7;
            }     
            g.drawImage(this.image, x, y,1280, 740,null);
            g.drawImage(g1, 890, 150,-486,470,null);//
            if(f2==true){
               if(z>=510){
                   f2=false;
               }
               z+=20;
            }
            else{
                if(f2==false){
                    z=500;
                    f2=true;
                    g10=g1;
                    g1=g2;
                    g2=g3;
                    g3=g4;
                    g4=g5;
                    g5=g6;
                    g6=g7;
                    g7=g8;
                    g8=g9;
                    g9=g10;
                }
            }
            if(f3==false){
                break;
            }
            try {
                Thread.sleep(50,5);
                g.clearRect(0, 50, 1280, 740);
            } 
            catch (InterruptedException ex) {
	    }
	}
     }
  if(btf==false){
        while(true){
            if(x<-4000){
                x=0;
 	    } 
            else{
                 x-=7;
            }
            g.drawImage(this.image, x, y,1280, 740,null);
             g.drawImage(g1, 400, 150,null);
            if(f4==false){
               if(v>=510){
                   f4=true;
               }
               v+=5;
            }
            else{
                if(f4==true){
                    v=500;
                    f4=false;
                    g9=g1;
                    g1=g2;
                    g2=g3;
                    g3=g4;
                    g4=g5;
                    g5=g6;
                    g6=g7;
                    g7=g8;
                    g8=g9;
                }
            }
            if(f3==true){
                break;
            }
            try {
                Thread.sleep(50,5);
                g.clearRect(0, 50, 1280, 740);
            } 
            catch (InterruptedException ex) {
	    }
            }
        }
    }
    public void playSound(String soundName){
        try
        {
            AudioInputStream audioInputStream = AudioSystem.getAudioInputStream(new File("C:\\Users\\taksin\\Downloads\\WALK\\CLICK1.mp3").getAbsoluteFile( ));
            Clip clip = AudioSystem.getClip( );
            clip.open(audioInputStream);
            clip.start( );
        }
        catch(Exception ex)
        {
            System.out.println("Error with playing sound.");
            ex.printStackTrace( );
        }
    }
}    

public class lab9 {
    public static void main(String[] args) throws IOException {
    JFrame f = new JFrame();
    f.add(new Panel());
    f.setSize(1280,740);
    f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    f.setVisible(true);
    }
}
