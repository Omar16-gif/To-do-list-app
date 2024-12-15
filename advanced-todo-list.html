import React, { useState, useRef } from 'react';
import { Card, CardHeader, CardTitle, CardContent } from '@/components/ui/card';
import { Button } from '@/components/ui/button';
import { Input } from '@/components/ui/input';
import { Tabs, TabsContent, TabsList, TabsTrigger } from '@/components/ui/tabs';
import { Dialog, DialogContent, DialogHeader, DialogTitle, DialogTrigger } from '@/components/ui/dialog';
import { 
  Plus, Trash2, UserPlus, Users, Upload, User, 
  Clock, Calendar, CheckCircle2 
} from 'lucide-react';

const TimePicker = ({ onTimeSelect, selectedTime }) => {
  const [startTime, setStartTime] = useState(selectedTime?.start || '');
  const [endTime, setEndTime] = useState(selectedTime?.end || '');

  const handleSave = () => {
    if (startTime && endTime) {
      onTimeSelect({ start: startTime, end: endTime });
    }
  };

  return (
    <div className="space-y-4 p-4">
      <div className="flex items-center space-x-2">
        <Clock className="text-gray-500" />
        <Input 
          type="time" 
          value={startTime}
          onChange={(e) => setStartTime(e.target.value)}
          className="flex-1"
          placeholder="Start Time"
        />
      </div>
      <div className="flex items-center space-x-2">
        <Calendar className="text-gray-500" />
        <Input 
          type="time" 
          value={endTime}
          onChange={(e) => setEndTime(e.target.value)}
          className="flex-1"
          placeholder="End Time"
        />
      </div>
      <Button onClick={handleSave} className="w-full">
        <CheckCircle2 className="mr-2" /> Set Timeline
      </Button>
    </div>
  );
};

const GoalTrackingApp = () => {
  const [users, setUsers] = useState([
    { 
      id: 1, 
      name: 'John Doe', 
      email: 'john@example.com',
      profilePic: '/api/placeholder/400/400',
    },
    { 
      id: 2, 
      name: 'Jane Smith', 
      email: 'jane@example.com',
      profilePic: '/api/placeholder/400/400',
    }
  ]);

  const [goals, setGoals] = useState({
    1: {
      videoUrl: '',
      todoList: [
        { id: 1, text: 'Study for midterms', completed: false, timeline: null },
        { id: 2, text: 'Exercise 30 minutes', completed: false, timeline: null }
      ]
    },
    2: {
      videoUrl: '',
      todoList: [
        { id: 1, text: 'Finish project', completed: false, timeline: null },
        { id: 2, text: 'Read a book', completed: false, timeline: null }
      ]
    }
  });

  const [errors, setErrors] = useState({});
  const [selectedUser, setSelectedUser] = useState(users[0].id);
  const [newUser, setNewUser] = useState({ name: '', email: '', profilePic: '' });
  const [newTodo, setNewTodo] = useState('');
  const [selectedTodoForTimeline, setSelectedTodoForTimeline] = useState(null);
  const [activeTab, setActiveTab] = useState("users");

  const handleAddUser = () => {
    // Validate user input
    if (!newUser.name.trim() || !newUser.email.trim()) {
      setErrors({ user: "Name and email are required" });
      return;
    }

    const newUserId = users.length + 1;
    const newUserEntry = {
      id: newUserId,
      name: newUser.name,
      email: newUser.email,
      profilePic: newUser.profilePic || '/api/placeholder/400/400'
    };

    setUsers(prev => [...prev, newUserEntry]);
    
    // Initialize goals for the new user
    setGoals(prev => ({
      ...prev,
      [newUserId]: {
        videoUrl: '',
        todoList: []
      }
    }));

    // Reset form and switch to users tab
    setNewUser({ name: '', email: '', profilePic: '' });
    setActiveTab("users");
    setSelectedUser(newUserId);
  };

  const handleAddTodo = () => {
    // Reset errors
    setErrors({});

    // Validate todo
    if (!newTodo.trim()) {
      setErrors({ todo: "Todo cannot be empty" });
      return;
    }

    setGoals(prev => ({
      ...prev,
      [selectedUser]: {
        ...prev[selectedUser],
        todoList: [
          ...(prev[selectedUser]?.todoList || []),
          { 
            id: Date.now(), 
            text: newTodo, 
            completed: false,
            timeline: null
          }
        ]
      }
    }));
    setNewTodo('');
  };

  const handleTimelineSelect = (time) => {
    if (selectedTodoForTimeline && selectedUser) {
      setGoals(prev => ({
        ...prev,
        [selectedUser]: {
          ...prev[selectedUser],
          todoList: prev[selectedUser].todoList.map(todo => 
            todo.id === selectedTodoForTimeline 
              ? { ...todo, timeline: time } 
              : todo
          )
        }
      }));
      setSelectedTodoForTimeline(null);
    }
  };

  return (
    <div className="container mx-auto p-4 max-w-4xl">
      <div className="bg-white dark:bg-gray-900 shadow-2xl rounded-2xl overflow-hidden">
        <Tabs 
          value={activeTab} 
          onValueChange={setActiveTab} 
          className="w-full"
        >
          <TabsList className="grid grid-cols-3 bg-gray-100 dark:bg-gray-800 p-1 rounded-none">
            <TabsTrigger 
              value="users" 
              className="data-[state=active]:bg-white data-[state=active]:text-black dark:data-[state=active]:bg-gray-700"
            >
              <Users className="mr-2" /> Users
            </TabsTrigger>
            <TabsTrigger 
              value="add-user"
              className="data-[state=active]:bg-white data-[state=active]:text-black dark:data-[state=active]:bg-gray-700"
            >
              <UserPlus className="mr-2" /> Add User
            </TabsTrigger>
            <TabsTrigger 
              value="user-goals"
              className="data-[state=active]:bg-white data-[state=active]:text-black dark:data-[state=active]:bg-gray-700"
            >
              <User className="mr-2" /> Goals
            </TabsTrigger>
          </TabsList>

          {/* Users List Tab */}
          <TabsContent value="users" className="p-4">
            <Card className="border-none shadow-none">
              <CardHeader className="px-0">
                <CardTitle className="text-2xl font-bold text-gray-800 dark:text-white">
                  Team Members
                </CardTitle>
              </CardHeader>
              <CardContent className="px-0">
                <div className="space-y-4">
                  {users.map((user) => (
                    <div 
                      key={user.id} 
                      className={`
                        p-4 rounded-xl cursor-pointer transition-all duration-300 
                        hover:bg-gray-100 dark:hover:bg-gray-800 
                        flex items-center 
                        ${selectedUser === user.id 
                          ? 'bg-blue-50 dark:bg-blue-900/30 ring-2 ring-blue-500/50' 
                          : 'bg-white dark:bg-gray-900'}
                      `}
                      onClick={() => {
                        setSelectedUser(user.id);
                        setActiveTab("user-goals");
                      }}
                    >
                      <img 
                        src={user.profilePic} 
                        alt={`${user.name}'s profile`} 
                        className="w-16 h-16 rounded-full mr-4 object-cover shadow-md"
                      />
                      <div>
                        <div className="font-semibold text-lg text-gray-800 dark:text-white">
                          {user.name}
                        </div>
                        <div className="text-sm text-gray-500 dark:text-gray-400">
                          {user.email}
                        </div>
                      </div>
                    </div>
                  ))}
                </div>
              </CardContent>
            </Card>
          </TabsContent>

          {/* Add User Tab */}
          <TabsContent value="add-user" className="p-4">
            <Card className="border-none shadow-none">
              <CardHeader className="px-0">
                <CardTitle className="text-2xl font-bold text-gray-800 dark:text-white">
                  Add New User
                </CardTitle>
              </CardHeader>
              <CardContent className="px-0 space-y-4">
                {errors.user && (
                  <div className="text-red-500 mb-4">{errors.user}</div>
                )}
                <Input 
                  placeholder="Name" 
                  value={newUser.name}
                  onChange={(e) => setNewUser(prev => ({ ...prev, name: e.target.value }))}
                  className="w-full"
                />
                <Input 
                  placeholder="Email" 
                  value={newUser.email}
                  onChange={(e) => setNewUser(prev => ({ ...prev, email: e.target.value }))}
                  className="w-full"
                />
                <Button onClick={handleAddUser} className="w-full">
                  <UserPlus className="mr-2" /> Add User
                </Button>
              </CardContent>
            </Card>
          </TabsContent>

          {/* Selected User's Goal Details */}
          <TabsContent value="user-goals" className="p-4">
            <Card className="border-none shadow-none">
              <CardHeader className="px-0 flex flex-row items-center justify-between">
                <CardTitle className="text-2xl font-bold text-gray-800 dark:text-white">
                  {users.find(u => u.id === selectedUser)?.name}'s Goals
                </CardTitle>
                <div className="flex items-center space-x-2">
                  <Input 
                    placeholder="New Todo" 
                    value={newTodo}
                    onChange={(e) => setNewTodo(e.target.value)}
                    className="w-full"
                  />
                  <Button onClick={handleAddTodo} variant="outline">
                    <Plus className="mr-2" /> Add
                  </Button>
                </div>
              </CardHeader>
              {errors.todo && (
                <div className="text-red-500 mb-4 px-4">{errors.todo}</div>
              )}
              <CardContent className="px-0 space-y-6">
                {goals[selectedUser]?.todoList?.map((todo) => (
                  <div 
                    key={todo.id} 
                    className="bg-gray-50 dark:bg-gray-800 p-4 rounded-xl flex items-center justify-between"
                  >
                    <div className="flex items-center space-x-4">
                      <input 
                        type="checkbox"
                        checked={todo.completed}
                        onChange={() => {
                          setGoals(prev => ({
                            ...prev,
                            [selectedUser]: {
                              ...prev[selectedUser],
                              todoList: prev[selectedUser].todoList.map(t => 
                                t.id === todo.id ? { ...t, completed: !t.completed } : t
                              )
                            }
                          }));
                        }}
                        className="h-5 w-5 text-blue-600 rounded focus:ring-blue-500"
                      />
                      <span 
                        className={`text-lg ${todo.completed ? 'line-through text-gray-500' : 'text-gray-800 dark:text-white'}`}
                      >
                        {todo.text}
                      </span>
                    </div>
                    <div className="flex items-center space-x-2">
                      {todo.timeline && (
                        <div className="text-sm text-gray-500 dark:text-gray-400 mr-2">
                          {todo.timeline.start} - {todo.timeline.end}
                        </div>
                      )}
                      <Dialog>
                        <DialogTrigger asChild>
                          <Button 
                            variant="outline" 
                            size="sm"
                            onClick={() => setSelectedTodoForTimeline(todo.id)}
                          >
                            <Clock className="h-4 w-4 mr-2" /> Timeline
                          </Button>
                        </DialogTrigger>
                        <DialogContent>
                          <DialogHeader>
                            <DialogTitle>Set Timeline for "{todo.text}"</DialogTitle>
                          </DialogHeader>
                          <TimePicker 
                            onTimeSelect={handleTimelineSelect} 
                            selectedTime={todo.timeline}
                          />
                        </DialogContent>
                      </Dialog>
                      <Button 
                        variant="ghost" 
                        size="sm"
                        onClick={() => {
                          setGoals(prev => ({
                            ...prev,
                            [selectedUser]: {
                              ...prev[selectedUser],
                              todoList: prev[selectedUser].todoList.filter(t => t.id !== todo.id)
                            }
                          }));
                        }}
                      >
                        <Trash2 className="h-4 w-4" />
                      </Button>
                    </div>
                  </div>
                ))}
              </CardContent>
            </Card>
          </TabsContent>
        </Tabs>
      </div>
    </div>
  );
};

export default GoalTrackingApp;
