package com.api.crud.MERCAFACIL.controller;
// Esta clase es un controlador REST que maneja las solicitudes HTTP relacionadas con los usuarios, 
// como obtener todos los usuarios,
import java.util.ArrayList;
import java.util.Optional;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import com.api.crud.MERCAFACIL.models.UserModel;
import com.api.crud.MERCAFACIL.services.UserService;
// para manejar las solicitudes HTTP relacionadas con los usuarios, como obtener todos los usuarios, 
// obtener un usuario por ID, crear un nuevo usuario, actualizar un usuario existente y eliminar un usuario.
@RestController
@CrossOrigin(origins = "*")
@RequestMapping("/users")
public class UserController {
    @Autowired
    private UserService userService;

 // para obtener todos los usuarios
@GetMapping
public ArrayList<UserModel> getAllUsers() {
    return userService.getUsers();
}
//para obtener un usuario por ID
@GetMapping(path = "/{id}")
public Optional<UserModel> getUserById(@PathVariable Long id) {
    return userService.getUserById(id);
}
// para crear un nuevo usuario
@PostMapping
public UserModel createUser(@RequestBody UserModel user) {
    return userService.createUser(user);
}
// para actualizar un usuario existente por ID
@PutMapping(path = "/{id}")
public UserModel userModelpdateUserById(@RequestBody UserModel request, @PathVariable Long id) {
    return userService.updateById(request, id);
}
// para eliminar un usuario por ID  
@DeleteMapping(path = "/{id}")
public String deleteUserById(@PathVariable Long id) {
        if (userService.deleteUser(id)) 
            return "User deleted Successfully";
    else
            return "User not found";
}

}
