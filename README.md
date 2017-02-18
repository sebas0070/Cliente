# Cliente
import java.net.DatagramPacket;
import java.net.DatagramSocket;

public class Cliente {

	/**
	 * @param args
	 */
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		int cliente;
		String tipo_cliente=args[0];
		String ip_servidor=args[1];
		int puerto=Integer.parseInt(args[2]);
		System.out.println(tipo_cliente+"  "+ip_servidor+"  "+puerto);
		cliente=comprobar_cliente(tipo_cliente);
		
		if(cliente==1){
			System.out.println("Se va enviar el paquete.");
			fugaz( ip_servidor, tipo_cliente, puerto);
			
		}
		else if(cliente==2){
			System.out.println("Entra en persistente.");
			persistente(ip_servidor, tipo_cliente, puerto);
			
		}
		else if(cliente==0){
			System.out.println("Error en comando, vuelva a ejecutar.");
			System.exit(-1);
		}
		
		
		
		
		
	}
	//Se comprueba el tipo de cliente que es.
	
	public static int  comprobar_cliente(String tipo_cliente){
		String tipo1="-udp";String tipo2="-tcp";
		if(tipo_cliente.equalsIgnoreCase(tipo1)){
			System.out.println("El cliente es fugaz.");
			
			return 1;
		}
		else if(tipo_cliente.equalsIgnoreCase(tipo2)){
			System.out.println("El cliente es persistente.");
			return 2;
		}
		else{
			System.out.println("Cliente inexistente.");
			return 0;
		}
		
	}
	
	public static void fugaz(String ip_servidor,String tipo_cliente,int puerto){
		Cliente_fugaz cl1=new Cliente_fugaz();
		cl1.setIp_servidor(ip_servidor);
		cl1.setPuerto(puerto);
		cl1.setTipo_cliente(tipo_cliente);
		cl1.conectar();
		//System.out.println(cl1.getMensaje_imprimir());
	}
	
	public static void persistente(String ip_servidor,String tipo_cliente,int puerto){
		Cliente_persistente cp1=new Cliente_persistente();
		cp1.setIp_servidor(ip_servidor);
		cp1.setPuerto(puerto);
		cp1.setTipo_cliente(tipo_cliente);
		cp1.conecta();
		
	}
	

	
}
