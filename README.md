# Frontrnd-FramwiseAI
npx create-react-app dynamic-fields-app
cd dynamic-fields-app
npm install react-redux redux
//
export const addField = (field) => ({
  type: 'ADD_FIELD',
  payload: field,
});
export const resetFields = () => ({
  type: 'RESET_FIELDS',
});
//
const initialState = {
  fields: [],
};

const fieldReducer = (state = initialState, action) => {
  switch (action.type) {
    case 'ADD_FIELD':
      return {
        ...state,
        fields: [...state.fields, action.payload],
      };
    case 'RESET_FIELDS':
      return {
        ...state,
        fields: [],
      };
    default:
      return state;
  }
};

export default fieldReducer;
//
import { createStore } from 'redux';
import fieldReducer from './reducers';
const store = createStore(fieldReducer);
export default store;
//
import React, { useState } from 'react';
import { useDispatch } from 'react-redux';
import { addField } from '../actions';

const AddFields = () => {
  const dispatch = useDispatch();
  const [field, setField] = useState({
    name: '',
    type: 'text',
    validation: '',
    data: '',
  });

  const handleInputChange = (e) => {
    const { name, value } = e.target;
    setField({ ...field, [name]: value });
  };

  const handleAddField = () => {
    dispatch(addField(field));
    setField({
      name: '',
      type: 'text',
      validation: '',
      data: '',
    });
  };

  return (
    <div>
      <h2>Add Fields</h2>
      {/* Dropdown and input fields go here */}
      <button onClick={handleAddField}>Add Field</button>
    </div>
  );
};

export default AddFields;
//import React from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { resetFields } from '../actions';

const DisplayFields = () => {
  const fields = useSelector((state) => state.fields);
  const dispatch = useDispatch();

  return (
    <div>
      <h2>Display Fields</h2>
      {/* Display added fields dynamically */}
      <button onClick={() => dispatch(resetFields())}>Reset Fields</button>
    </div>
  );
};

export default DisplayFields;
//import React from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { resetFields } from '../actions';

const DisplayFields = () => {
  const fields = useSelector((state) => state.fields);
  const dispatch = useDispatch();

  return (
    <div>
      <h2>Display Fields</h2>
      {/* Display added fields dynamically */}
      <button onClick={() => dispatch(resetFields())}>Reset Fields</button>
    </div>
  );
};

export default DisplayFields;
//import React from 'react';
import AddFields from './components/AddFields';
import DisplayFields from './components/DisplayFields';

function App() {
  return (
    <div>
      <AddFields />
      <DisplayFields />
    </div>
  );
}

export default App;
//
npm start



