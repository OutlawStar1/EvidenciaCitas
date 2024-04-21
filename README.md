# Proyecto Administracion de citas de Consultorio Dental
Creacion de usuarios/pacientes
Creacion de citas
Eliminar uaurios y citas
Administrar citas

Codigo de la aplicacion

index.jsp
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<%@ page import="controler.almacenPaciente" %>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Creacion de paciente</title>
</head>
	<body>
		<div>
			<h1>Crear Paciente</h1>
			<form action="almacenPaciente" method="post">
				Nombre: <br>
				<input type="text" name= "nombre" value=""><br>
				Apellido: <br>
				<input type= "text" name= "apellido" value=""><br><br>
				Numero de Telefono: <br>
				<input type= "text" name= "numero_telefono" value=""><br><br>
				<input type= "submit" value="Crear Paciente">
				
			</form>
		</div>
	</body>
</html>

retornoPaciente.jsp

<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<%@ page import="consultoria.Paciente" %>
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8">
	<title>Calculo IMC</title>
</head>
	<body>
	<% Paciente P = (Paciente) request.getAttribute("pacienteCreado"); %>
		<h1>Paciente Nuevo: </h1>
		(<%= P.getNombre()%>) (<%= P.getApellido()%>)  (<%= P.getNumero_telefono()%>) es <%= P.getApaciente() %><br>
		
		<a href = "index.jsp">¿Crear otro Paciente?</a>
	</body>
</html>

Paciente.java

package consultoria;

public class Paciente{
	
	private String nombre;
	private String apellido;
	private String numero_telefono;
	private String apaciente;
	
	
	
	public Paciente(String n, String a, String t) {
		this.setNombre((n));
		this.setApellido((a));
		this.setNumero_telefono((t));
    }
	
	public void hacerApaciente() {
		String P = (this.getNombre() + " " + this.getApellido() + " " + this.getNumero_telefono());
		this.setApaciente(P);
	}
	
	public String getNombre() {
		return nombre;
	}
	
	public void setNombre(String nombre) {
		this.nombre = nombre;
	}
	
	public String getApellido() {
		return apellido;
	}
	
	public void setApellido(String apellido) {
		this.apellido = apellido;
	}
	
	public String getNumero_telefono() {
		return numero_telefono;
	}
	
	public void setNumero_telefono(String numero_telefono) {
		this.numero_telefono = numero_telefono;
	}
	
	public String getApaciente() {
		return apaciente;
	}
	
	public void setApaciente(String apaciente) {
		this.apaciente = apaciente;
	}
}

almacenPaciente.java

package controler;

import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/almacenPaciente")
public class almacenPaciente extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    
	protected void processRequest(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException{
		response.setContentType("text/html;charset=UFT-8");
		String n=request.getParameter("nombre");
		String a=request.getParameter("apellido");
		String t=request.getParameter("numero_telefono");
		consultoria.Paciente P = new consultoria.Paciente(n, a, t);
		P.hacerApaciente();
		request.setAttribute("pacienteCreado", P);
		request.getRequestDispatcher("/retornoPaciente.jsp").forward(request, response);
	}

	@Override
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		/*response.getWriter().append("Served at: ").append(request.getContextPath());
		* 
		*/
	}

	@Override
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		//doGet(request, response);
		processRequest(request,response);
		
	}
	
	@Override
	public String getServletInfo() {
		return "Pacientes Existentes";
	}

}
