CREATE DEFINER=`root`@`localhost` TRIGGER `factura_AFTER_INSERT` AFTER INSERT ON `factura` FOR EACH ROW BEGIN
DECLARE puntajeActual int;
DECLARE nuevoPuntaje int;

    set puntajeActual = (select puntaje from clientes where cedula = NEW.idCliente);
    set nuevoPuntaje = puntajeActual +  10;
    
	update clientes
    set puntaje = nuevoPuntaje
    where cedula = NEW.idCliente; 
END
