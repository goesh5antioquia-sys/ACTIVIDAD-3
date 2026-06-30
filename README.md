package com.api.crud.MERCAFACIL.controller;

import java.util.ArrayList;
import java.util.Optional;

import org.springframework.beans.factory.annotation.Autowired;
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

@RestController
@RequestMapping("/users")
public class UserController {
    @Autowired
    private UserService userService;

 
@GetMapping
public ArrayList<UserModel> getAllUsers() {
    return userService.getUsers();
}

@GetMapping(path = "/{id}")
public Optional<UserModel> getUserById(@PathVariable Long id) {
    return userService.getUserById(id);
}
@PostMapping
public UserModel createUser(@RequestBody UserModel user) {
    return userService.createUser(user);
}
@PutMapping(path = "/{id}")
public UserModel userModelpdateUserById(@RequestBody UserModel request, @PathVariable Long id) {
    return userService.updateById(request, id);
}
@DeleteMapping(path = "/{id}")
public String deleteUserById(@PathVariable Long id) {
        if (userService.deleteUser(id)) 
            return "User deleted Successfully";
    else
            return "User not found";
}

}
